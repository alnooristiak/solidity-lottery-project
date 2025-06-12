# 🎯 Solidity Lottery Smart Contract | Ethereum DApp for Beginners

![Solidity](https://img.shields.io/badge/Solidity-0.8.x-blue.svg)
![License](https://img.shields.io/badge/License-GPL--3.0-green.svg)
![Open Source Love](https://img.shields.io/badge/Open%20Source-%E2%9D%A4-red.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)
![Made with ❤️ in Bangladesh](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%EF%B8%8F-in%20Bangladesh-orange)

A beginner-friendly yet powerful **Ethereum Lottery Smart Contract** built using **Solidity**...

> ✅ Perfect for your **Web3 Portfolio**, GitHub profile, or as a base project for interviews and freelance work.

---

## 🚀 Why This Project?

If you're a beginner in blockchain or smart contract development, this project is a **must-have** in your portfolio. It covers the basics of Solidity, real ETH transfers, contract logic, and access restrictions.

---

## 📌 Key Features of the Ethereum Lottery DApp

- 🎫 **1 ETH Entry System** — Only 1 ETH per entry is allowed
- 🧑‍💼 **Manager Control** — Only the contract manager can select the winner
- 🎲 **Random Winner Selection** — Uses block metadata and participant count to generate randomness
- 💸 **Automatic ETH Transfer** — Winner receives all ETH instantly
- 🔁 **Participant Reset** — The game resets after each winner selection

---

## 🔧 Tech Stack & Tools Used

| Technology | Description                               |
| ---------- | ----------------------------------------- |
| Solidity   | Smart contract programming language       |
| Ethereum   | Blockchain platform                       |
| Remix IDE  | Online IDE for smart contract development |
| MetaMask   | Wallet to interact with the contract      |

---

## 📂 How It Works (Step-by-Step)

1. The contract is deployed by the **manager**.
2. Users join the lottery by sending exactly **1 ETH**.
3. Once **3 or more participants** join, the manager triggers winner selection.
4. A **pseudo-random number** is generated using:
   - `block.prevrandao`
   - `block.timestamp`
   - `participants.length`
5. ETH is transferred to the randomly selected participant.
6. The game **resets** for the next round.

---

## 📘 Smart Contract Functions

| Function         | Access       | Purpose                                                 |
| ---------------- | ------------ | ------------------------------------------------------- |
| `receive()`      | Public       | Accepts exactly 1 ETH per participant                   |
| `getBalance()`   | Manager Only | Shows the contract balance in Wei                       |
| `random()`       | Public View  | Generates a pseudo-random number                        |
| `selectWinner()` | Manager Only | Selects a winner and sends the ETH, resets participants |

---

## 🧪 Try It Yourself (Testing Instructions)

1. Open [Remix IDE](https://remix.ethereum.org/)
2. Paste the smart contract code
3. Use compiler version `^0.5.2 <0.9.0`
4. Deploy with any test account (you will be the manager)
5. Use multiple test accounts to send exactly `1 ETH`
6. When 3+ users have joined, call `selectWinner()` from the manager

---

## 🧠 Smart Contract Code Summary

```solidity
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.5.2 <0.9.0;

contract Lottery {
    address public manager;
    address payable[] public participants;

    constructor() {
        manager = msg.sender;
    }

    receive() external payable {
        require(msg.value == 1 ether);
        participants.push(payable(msg.sender));
    }

    function getBalance() public view returns (uint) {
        require(msg.sender == manager);
        return address(this).balance;
    }

    function random() public view returns (uint) {
        return uint(keccak256(abi.encodePacked(block.prevrandao, block.timestamp, participants.length)));
    }

    function selectWinner() public {
        require(msg.sender == manager);
        require(participants.length >= 3);
        uint r = random();
        address payable winner = participants[r % participants.length];
        winner.transfer(getBalance());
        participants = new address payable ;
    }
}
```

## 🚀 Future Enhancements (Optional Ideas)

- Integrate with a frontend using React/Web3.js.
- Use Chainlink VRF for secure randomness.
- Add time-based or round-based lottery control.
- Implement audit and security checks.

---

## 🧑‍💻 About Me

I'm a passionate **Solidity Smart Contract Developer** from **Dhaka, Bangladesh**.
I focus on **Web3, DeFi, and blockchain security**.
This project is part of my **open-source contributions** to help others learn and grow in the Ethereum ecosystem.

🔗 **Connect With Me**

- [GitHub: @alnooristiak](https://github.com/alnooristiak)
- [Twitter: @alnooristiak](https://twitter.com/alnooristiak)
- [LinkedIn: @alnooristiak](https://linkedin.com/in/alnooristiak)
