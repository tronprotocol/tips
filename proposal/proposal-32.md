Dear Developers,  

No. 29 voting request was initiated to vote on No. 32 proposal at 11:30, February 21, 2020 (Singapore time). 

After the proposal is approved, three new features of TVM (TRON Virtual Machine) will be opened: support for parallel signature verification, multi signature verification, and judge whether the address is the contract address.

After the proposal is approved, it will further enrich the application scenarios of smart contracts.

Next, I'd like to give you a detailed introduction of the use scenarios of these three new features and what should be noted.

**1.Support parallel signature verification in TVM**

The 'batchvalidatesign' keyword can be used in the contract for parallel signature verification:

```
batchvalidatesign(bytes32 hash, bytes[] signatures, address[] addresses)
```

Example:

```
pragma experimental ABIEncoderV2;
contract Demo {
    function testBatch(bytes32 hash, bytes[] memory signatures, address[] memory addresses) public returns(bytes32){
        return batchvalidatesign(hash, signatures, addresses);
    }
}
```

Because 'batchvalidatesign' is implemented by the precompiled contract (0x9) in TVM, it can also be used in the following way:

```
function testBatch(bytes memory data) public returns(bool, bytes memory){
    return address(0x9).delegatecall(data); // data is a parameter that needs to be spliced by itself
}
```

This new feature can be used to support multiple users to sign the same data content (hash).

'batchvalidatesign' can verify up to 16 signatures at the same time.

'batchvalidatesign' consumes 1500 energy to verify per signature. If 5 signatures are verified at the same time, 1500*5 = 7500 energy will be consumed.

**2.Support to judge whether the address is a contract address in TVM**

In the development of smart contracts, developers may often encounter the situation of calling another contract in a contract, but some contracts may not want to be invoked by other contracts, and the call can be restricted by using 'isContract'. 

For example:

```
pragma solidity ^0.5.9;
contract Lib{
    modifier onlyHuman {
        require(!msg.sender.isContract, "contract address is restricted");
        _;
    }
}

contract Core is Lib{
    constructor () public  {
    }
    function do_some_thing() internal {}
    function call_a_function()  public onlyHuman returns (bool){
        do_some_thing();
        return true;
    }
}
contract Client {
    Core core;
    constructor () public  {
        core = new Core();
    }
    function call_core()  public {
        //This will revert because onlyHuman
    core.call_a_function();
    }
}
```

**3.Support multi signature verification in TVM**

TRON blockchain supports the multi signature feature of the account, and is widely used in scenarios such as permission control. This time, multi signature feature is also supported in TVM.

In the contract, you can use the 'validatemultisign' keyword for multi signature verification.

```
validatemultisign(address accountAddress, uint256 permissionId, bytes32 content, bytes[] signatures)
```

The following example is an application scenario using a multi signature account to transfer to other accounts:

```
pragma experimental ABIEncoderV2;
contract safeVaultDemo {

    constructor() public payable {
        //can deposit here
    }

    function withDraw(address a, uint256 perid, bytes32 hash, bytes[] memory signatures, address payable toAddress ,uint amount) public{
        require(validatemultisign(a, perid, hash, signatures), "validate multiSign error");
        //transfer TRX
        toAddress.transfer(amount);
    }
}
```

Since 'validatemultisign' is also implemented by the precompiled contract (0xa) in TVM, it can also be used as follows:

```
function withDraw(bytes memory data, address payable toAddress ,uint amount) public returns(bool, bytes memory){
    require(address(0xa).delegatecall(data), "validate multiSign error"); // data is a parameter that needs to be spliced by itself
    //transfer TRX
    toAddress.transfer(amount);
}
```

Multi signatures can only support signatures of up to five private keys.

'validatemultisign' consumes 1500 energy to verify per signature. If three signatures are verified at the same time, 1500 * 3 = 4500 energy will be consumed.

If you have any question, please leave a comment.
