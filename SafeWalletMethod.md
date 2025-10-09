# 🔐 Safe Wallet Method

A secure method to encrypt and protect crypto wallet recovery phrases (seed phrases).  
Designed by **ali & chatgpt**  
🌍 Open Source Project – MIT License

---

## 🧩 Overview

The **Safe Wallet Method** is a mathematical encryption approach based on the **BIP39** standard.  
It allows you to store your recovery phrase in a disguised form — easy to recover but impossible to guess without your private key number.

---

## ⚙️ How It Works

1. Take your original recovery phrase (e.g., 12 or 24 BIP39 words).  
2. Find each word’s **number index** from the official [BIP39 wordlist](https://github.com/bitcoin/bips/blob/master/bip-0039/english.txt).  
3. Choose a **personal constant number** — for example, part of your bank account, birthday digits, or a secret code.  
4. **Add** this constant number to each word’s index.  
5. Use the resulting numbers to **find the new words** from the BIP39 list.  
6. Save the new list — this becomes your **encrypted seed phrase**.  
7. To recover, simply **subtract** the same constant number and map back to the original words.

---

## 🧠 Example

Let’s say one of your words is number **200** in the BIP39 list.  
Your secret number is **50**.  
200 + 50 = 250  
Now, word number **250** becomes your **encrypted version**.

---

## ⚠️ Important Notes

- Never share or lose your secret constant number.  
- Without that number, your real wallet **cannot be recovered**.  
- This method is 100% offline and doesn’t require any app or internet access.  
- It increases security against phishing, hacking, or data leaks.

---

## 💡 Advantages

- Works fully **offline**  
- No software required  
- **Compatible** with all BIP39-based wallets (TronLink, MetaMask, Trust Wallet, etc.)  
- Simple but highly secure  
- Perfect for long-term backup

---

## 🏷️ Authors

👤 **Ali**  
🤖 **ChatGPT**

Team: **ali & chatgpt**  
GitHub: [https://github.com/alichatme](https://github.com/alichatme)

---

## 📄 License

**MIT License – 2025**  
Open-source for educational and personal use.
