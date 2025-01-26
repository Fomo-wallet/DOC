# FOMOWallet - Betting on the Future of Cryptocurrency

---

## **Project Introduction**

Welcome to FOMOWallet, where you can bet, and even if you don't make the guesses right, you'll still get paid if your bet guesses are closer to the original target. This is a blockchain-powered number-guessing game where privacy meets fun. The game leverages cutting-edge technologies like the Lit Protocol for encryption, smart contracts on the Mantle blockchain, and AI-driven feedback to keep things interesting and secure.

Players guess a target number (which is encrypted) and get AI-powered hints along the way. Social integrations like Twitter updates and email notifications keep everyone in the loop. If you're into blockchain, AI, and a bit of friendly competition, you’re in the right place!

---

## **Mantle Contract Addresses**

- **BETTING CONTRACT ADDRESS: 0x8Ee9cE6002cc654c59AE7eA36Cf25226bb8cD73C
- **USDT CONTRACT ADDRESS: 0xe8D926e2B3bDb668CeFf6773564441C4029F9Da6

## **Core Features**

---

- **💸 Decentralized Betting:** Place bets on the Mantle blockchain and get rewarded for correct guesses.
- **🔒 Encrypted Numbers with Lit Protocol:** Target numbers are securely encrypted using Lit Protocol.
- **🧠 AI Feedback:** Get real-time AI hints on whether your guess is getting “warmer” or “colder.”
- **📢 Social Updates:** Receive game alerts through Twitter and email notifications.
- **📊 Real-time Data:** Subgraphs track game stats and player performance.

---

## **Technical Architecture**

- **Blockchain:** Smart contracts deployed on the Mantle chain.
- **Encryption:** Target numbers encrypted using Lit Protocol.
- **Indexing:** Subgraphs via The Graph Protocol for real-time data.
- **AI Feedback:** AI agents analyze guesses and provide hints.
- **Notifications:** Twitter and email keep everyone updated.

---

## **Smart Contracts**

### **1. Encrypted Number Storage**

We use Lit Protocol to encrypt the target number before storing it on-chain. This ensures that no one (not even the contract itself) can see the number until the game ends.

**Example Code:**

```solidity
// EncryptedNumberStorage.sol
function storeEncryptedNumber(bytes memory encryptedNumber) public {
    encryptedTarget = encryptedNumber;
}
```

Wanna learn more? [smart contracts repository](https://github.com/Fomo-wallet/fomoWallet-contracts)

### **2. Betting Mechanics**

Players place bets by submitting their guesses. The smart contract verifies the guesses securely and manages the rewards.

**Betting Function:**

```solidity
// BettingLogic.sol
function placeBet(uint256 guess) public payable {
    require(msg.value >= minBetAmount, "Bet amount too low");
    emit BetPlaced(msg.sender, guess);
}
```

### **3. AI Feedback Integration**

When a guess is placed, the contract emits an event, which triggers the AI agent to analyze the guess and provide feedback.

**Feedback Event:**

```solidity
// AIIntegration.sol
event AIResponseEmitted(address indexed user, string feedback);
```

### **4. Security Measures**

- **Lit Protocol Encryption:** Keeps target numbers private.
- **Secure Betting:** Validates bets and prevents tampering.
- **Escrow System:** Holds funds until a winner is determined.

---

## 🤖 **AI Agents**

### **How AI Feedback Works**

- **Proximity Analysis:** The AI compares your guess to the encrypted target and gives you hints like “warmer” or “colder.”
- **Confidence Score:** The AI shares how confident it is in the feedback.
- **Suggestions:** Optional hints for your next guess.

### **AI Response Example:**

```typescript
interface AIResponse {
  proximity: string;        // "warmer" or "colder"
  confidence: number;       // e.g., 0.85
  suggestion: string;       // e.g., "Try a higher number"
}
```

### **Social Integration**

- **Twitter Alerts:** Game updates and results are posted automatically.
- **Email Notifications:** Get personalized updates directly in your inbox.

---

## 📊 **Subgraphs**

### **Schema Design**

We use The Graph Protocol to track bets and game status in real-time.

**GraphQL Schema:**

```graphql
type Bet @entity {
  id: ID!
  user: Bytes!
  guess: BigInt!
  timestamp: BigInt!
  feedback: String!
}

type Game @entity {
  id: ID!
  encryptedTarget: Bytes!
  status: String!
  winner: Bytes
}
```

### **Example Queries**

**Get All Bets by a User:**

```graphql
query GetUserBets($userAddress: Bytes!) {
  bets(where: { user: $userAddress }) {
    guess
    feedback
    timestamp
  }
}
```

**Get Active Games:**

```graphql
query GetActiveGames {
  games(where: { status: "active" }) {
    id
    encryptedTarget
  }
}
```

---

## 🔄 **Technical Documentation**

### **1. Installation Steps**

Clone the repository:

```bash
git clone https://github.com/Fomo-wallet/fomoWallet-contracts
cd fomoWallet-contracts
```

### **2. Environment Setup**

Copy the `.env` template and fill in your API keys:

```bash
cp .env.example .env
```

Add your keys:

```plaintext
MANTLE_RPC_URL=<your_mantle_rpc_url>
LIT_API_KEY=<your_lit_api_key>
TWITTER_API_KEY=<your_twitter_api_key>
EMAIL_API_KEY=<your_email_api_key>
```

### **3. Deploy Smart Contracts**

```bash
npx hardhat run scripts/deploy.js --network mantle
```

### **4. Deploy Subgraph**

```bash
graph deploy --studio [subgraph-name]
```

### **5. Testing**

**Smart Contract Tests:**

```bash
npx hardhat test
```

**AI Feedback Tests:**

```bash
npm run test:ai
```

**Integration Tests:**

```bash
npm run test:integration
```

---

## 📊 **Monitoring**

- **Subgraph Health:** Monitor through The Graph Studio.
- **AI Performance:** Track response times and accuracy.
- **Contract Activity:** Check MantleScan for on-chain activity.

---

## 🛠️ **Maintenance**

- **Regular Audits:** Ensure smart contracts are secure.
- **Subgraph Updates:** Keep indexing up-to-date.
- **AI Fine-Tuning:** Improve feedback accuracy over time.

---

## 🚀 **Future Improvements**

1. **Multi-Chain Support:** Expand to other EVM-compatible chains.
2. **Better AI Models:** Smarter feedback and predictions.
3. **Mobile App:** Play on the go!
4. **More Game Modes:** New challenges and variations.

---

## 🤝 **Contributing**

We’d love your help! Here's how to contribute:

1. **Fork the Repo**: Click the fork button.
2. **Create a Branch**: `git checkout -b feature-branch`
3. **Commit Your Changes**: `git commit -m "Add cool feature"`
4. **Push**: `git push origin feature-branch`
5. **Open a Pull Request**: We’ll review it and merge!

---

## 🐝 **License**

This project is licensed under the **MIT License**. Check out the `LICENSE` file for details.
