# Building a DAO

## What is a DAO?

DAO stands for **D**ecentralized **A**utonomous **O**rganization. You can think of DAOs as analogous to companies in the real world. Essentially, DAOs allow for members to create and vote on governance decisions.

In traditional companies, when a decision needs to be made, the board of directors or executives of the company are in charge of making that decision. In a DAO, however, this process is democratized, and any member can create a proposal, and all other members can vote on it. Each proposal created has a deadline for voting, and after the deadline the decision is made in favour of the voting outcome (YES or NO).

Membership in DAOs is typically restricted either by ownership of ERC20 tokens, or by ownership of NFTs. Examples of DAOs where membership and voting power is proportional to how many tokens you own include [Uniswap](https://uniswap.org) and [ENS](https://ens.domains). Examples of DAOs where they are based on NFTs include [Meebits DAO](https://www.meebitsdao.world/).

## Building our DAO

You want to launch a DAO for holders of your `Crypto Devs` NFTs. From the ETH that was gained through the ICO, you built up a DAO Treasury. The DAO now has a lot of ETH, but currently does nothing with it.

You want to allow your NFT holders to create and vote on proposals to use that ETH for purchasing other NFTs from an NFT marketplace, and speculate on price. Maybe in the future when you sell the NFT back, you split the profits among all members of the DAO.

## Requirements

- Anyone with a `Crypto Devs` NFT can create a proposal to purchase a different NFT from an NFT marketplace
- Everyone with a `Crypto Devs` NFT can vote for or against the active proposals
- Each NFT counts as one vote for each proposal
- Voter cannot vote multiple times on the same proposal with the same NFT
- If majority of the voters vote for the proposal by the deadline, the NFT purchase is automatically executed

## What we will make

- To be able to purchase NFTs automatically when a proposal is passed, you need an on-chain NFT marketplace that you can call a `purchase()` function on. There exist a lot of NFT marketplaces out there, but to avoid overcomplicating things, we will create a simplified fake NFT marketplace for this tutorial as the focus is on the DAO.
- We will also make the actual DAO smart contract using Hardhat.
- We will make the website using Next.js to allow users to create and vote on proposals

## Prerequisites

- You have completed the [NFT-Collection Tutorial](https://github.com/LearnWeb3DAO/NFT-Collection)
- You must have some ETH to give to the DAO Treasury

## BUIDL IT

### Smart Contract Development

We will start off with first creating the smart contracts. We will be making two smart contracts:

- `FakeNFTMarketplace.sol`
- `CryptoDevsDAO.sol`

To do so, we will use the [Hardhat](https://hardhat.org) development framework we have been using for the last few tutorials.

- Create a folder for this project named `DAO-Tutorial`, and open up a Terminal window in that folder.
- Setup a new hardhat project by running the following commands in your terminal:

  ```bash
  mkdir hardhat-tutorial
  cd hardhat-tutorial
  npm init --yes
  npm install --save-dev hardhat
  ```

  Now that you have installed Hardhat, we can setup a project. Execute the following command in your terminal.

- In the same directory where you installed Hardhat run:

  ```bash
  npx hardhat
  ```

  - Select `Create a Javascript project`
  - Press enter for the already specified `Hardhat Project root`
  - Press enter for the question on if you want to add a `.gitignore`
  - Press enter for `Do you want to install this sample project's dependencies with npm (@nomicfoundation/hardhat-toolbox)?`

    Now you have a hardhat project ready to go!

    If you are on Windows, please do this extra step and install these libraries as well :)

    ```bash
    npm install --save-dev @nomicfoundation/hardhat-toolbox
    ```

  and press `Enter` for all the questions (Choose the `Create a basic sample project`) option.

- Now, let's install the `@openzeppelin/contracts` package from NPM as we will be using [OpenZeppelin's Ownable Contract](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol) for the DAO contract.
  ```bash
  npm install @openzeppelin/contracts
  ```
- First, let's make a simple Fake NFT Marketplace. Create a file named `FakeNFTMarketplace.sol` under the `contracts` directory within `hardhat-tutorial`, and add the following code.

- Let's make sure everything compiles before we start writing the DAO Contract. Run the following command inside the `hardhat-tutorial` folder from your Terminal.
  ```bash
  npx hardhat compile
  ```
  and make sure there are no compilation errors.
- Now, we will start writing the `CryptoDevsDAO` contract. Since this is mostly a completely custom contract, and relatively more complicated than what we have done so far, we will explain this one bit-by-bit.
- First, let's write the boilerplate code for the contract. Create a new file named `CryptoDevsDAO.sol` under the `contracts` directory in `hardhat-tutorial` and add the following code to it.

 
