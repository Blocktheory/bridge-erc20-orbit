## Steps to Transfer ERC20 tokens from L2 to L3 for Orbit Chain

To set up the token deposit process for transferring ERC20 tokens between Layer 2 (L2) and Layer 3 (L3), follow these steps:

1. Clone the "bridge-erc20-orbit" repository:

git clone https://github.com/Blocktheory/bridge-erc20-orbit


2. Create a .env file in the root directory with the following fields:

```
//EXAMPLE
DEVNET_PRIVKEY="0x private key of your account"

//RPC URL of your appchain(L3)
L2RPC="http://127.0.0.1:8449"

//L1RPC is of goerli-arbitrum if you are building it on arbitrum mainnet change the RPC accordingly
L1RPC="https://goerli-rollup.arbitrum.io/rpc"

//Address of token on L2 which you want to transfer to L3
TOKEN_ADDRESS="0x Token address"


//Amount of tokens you want to send
AMOUNT=Token_Amount
```

3. Install dependencies in the root directory:

```yarn install```


4. Add details of the L2 chain you are using inside exports.l1Networks section inside networks.js file present in "node_modules/@arbitrum/sdk/dist/lib/dataEntities":

```// Example:
421613: {
        blockTime: 15,
        chainID: 421613,
        explorerUrl: 'https://goerli.arbiscan.io',
        isCustom: false,
        name: 'Arbitrum Goerli Testnet',
        partnerChainIDs: [421613],
        isArbitrum: false,
    },
```


5. In above file add details of your chain inside the l2Networks section in the same file:

```// Example
chainId: {
        chainID: 181,
        confirmPeriodBlocks: 30,
        ethBridge: {
            bridge: '0xbridge Address',
            inbox: '0xinbox Address',
            outbox: '0xoutbox Address',
            rollup: '0xrollup Address',
            sequencerInbox: '0xsequencer Address',
        },
        explorerUrl: 'http://localhost:4000/',
        isArbitrum: false,
        isCustom: true,
        name: 'Chain Name',

        partnerChainID: 42613,
        retryableLifetimeSeconds: constants_1.TWO_DAYS_IN_SECONDS,
        tokenBridge: {
            l1CustomGateway: '0xL2 Custom Gateway Address',
            l1ERC20Gateway: '0xL2 standardGateway address',
            l1GatewayRouter: '0xL2 router address',
            l1MultiCall: '0xL2 multicall address',
            l1ProxyAdmin: '0xL2 proxyAdmin address',
            l1Weth: '0xL2 weth address',
            l1WethGateway: '0xL2 wethGateway address',
            l2CustomGateway: '0xappchain customGateway address',
            l2ERC20Gateway: '0xappchain standardGateway address',
            l2GatewayRouter: '0xappchain router address',
            l2Multicall: '0xappchain multicall address',
            l2ProxyAdmin: '0xappchain proxyAdmin address',
            l2Weth: '0xappchain weth address',
            l2WethGateway: '0xappchain wethGateway address',
        },
        nitroGenesisBlock: 0,
        nitroGenesisL1Block: 0,
        /**
         * Finalization on mainnet can be up to 2 epochs = 64 blocks on mainnet
         * We add 10 minutes for the system to create and redeem the ticket, plus some extra buffer of time
         * (Total timeout: 30 minutes)
         */
        depositTimeout: 1800000,
    },
```

All the required addresses you already received when you ran the command to set-up the chain.

6. Run the token-deposit process:

```yarn run token-deposit```



A token minting process is occurring on Layer 2 (L2), followed by a transfer of 50 tokens to Layer 3 (L3). The "exec.js" script in the "token-deposit" Repo handles this operation, and modifying line 29 allows for adjusting the number of tokens transferred to L3. It's crucial to understand the blockchain network and token standards to ensure secure execution of the transfer process between L2 and L3.


