---
tip: 
title: Sovereign Checkout - Autonomous Self-Refunding Merchant Settlement Standard
author: Lambert Van Sittert (@Lambertvs)
status: Draft
type: Standards Track
category: TRC
created: 2026-11-01
---

## Simple Summary
A decentralized smart contract settlement standard for TRC-20 tokens that enforces atomic invoice settlement and provides autonomous self-refunds for underpaid or expired merchant deposits.

## Abstract
Current retail crypto payment integrations on TRON instruct payers to send TRC-20 tokens (such as USDT) to raw, unmonitored addresses managed by centralized payment gateways (e.g., BVNK). When minor underpayments or fee deductions occur, automated sweepers absorb the funds into multi-million dollar corporate master vaults, while backend merchant systems reject the deposit and declare funds "lost". 

This TIP standardizes a trustless, non-custodial merchant settlement contract where:
1. Invoices settle atomically upon full payment;
2. Underpaid funds remain held in smart contract escrow with zero merchant/gateway custody;
3. Payers can trigger an autonomous self-refund directly back to their nominated TRON address once an invoice expires.

## Motivation
Millions of dollars in TRC-20 retail transactions are lost or trapped annually because TRON's base TRC-20 standard lacks invoice-level settlement and refund logic. Centralized gateways exploit this vacuum by keeping underpaid deposits as unallocated corporate float. By establishing a standard smart contract checkout protocol on TRON, wallets and dApps can eliminate centralized payment traps entirely.

## Specification

### Interface
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

interface ITRC_SovereignCheckout {
    enum InvoiceStatus { Active, Settled, Refunded, Cancelled }

    struct Invoice {
        bytes32 invoiceId;
        address merchant;
        address payer;
        address refundAddress;
        address token;
        uint256 expectedAmount;
        uint256 amountPaid;
        uint256 expiryTimestamp;
        InvoiceStatus status;
    }

    event InvoiceCreated(bytes32 indexed invoiceId, address indexed merchant, address indexed token, uint256 expectedAmount, uint256 expiryTimestamp);
    event PaymentReceived(bytes32 indexed invoiceId, address indexed payer, uint256 amount, uint256 totalPaid, uint256 remaining);
    event InvoiceSettled(bytes32 indexed invoiceId, address indexed merchant, uint256 totalAmount);
    event AutonomousRefundClaimed(bytes32 indexed invoiceId, address indexed recipient, uint256 amountRefunded);

    function createInvoice(bytes32 invoiceId, address token, uint256 expectedAmount, uint256 durationSeconds) external;
    function payInvoice(bytes32 invoiceId, uint256 amount, address refundAddress) external;
    function claimRefund(bytes32 invoiceId) external;
    function merchantCancelAndRefund(bytes32 invoiceId) external;
}
```

## Implementation
Reference implementation is open-sourced at: https://github.com/Lambertvs/sovereign-payer-protocol

## Security Considerations
1. Re-entrancy protection is enforced by setting `status = Refunded` and zeroing `amountPaid` prior to the token transfer.
2. The contract holds zero admin keys or privileged backdoors.
