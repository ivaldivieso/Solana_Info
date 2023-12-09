## Information about files in solana

```
├─ src
│  ├─ lib.rs -> registering modules
│  ├─ entrypoint.rs -> entrypoint to the program
│  ├─ instruction.rs -> program API, (de)serializing instruction data
│  ├─ processor.rs -> program logic
│  ├─ state.rs -> program objects, (de)serializing state
│  ├─ error.rs -> program specific errors
├─ .gitignore
├─ Cargo.lock
├─ Cargo.toml
├─ Xargo.toml
```

## Agregar tu wallet test Phathom
- Referencia https://www.quicknode.com/guides/solana-development/getting-started/a-complete-guide-to-airdropping-test-sol-on-solana
- Referencia https://www.quicknode.com/guides/solana-development/getting-started/how-to-look-up-the-balance-of-a-solana-wallet
- Se requiere usar los siguientes comandos copiando la wallet y agregandola como dev

```
solana airdrop 1 9HekP9CfByCcDrfneqNR7BPgsNYob2woRaN3WqqS9tKP -u devnet
```
Donde 9Hek.. es mi wallet 

- Para usar un script podemos usar el siguiente, asi interactuamos:
```
const SOLANA = require('@solana/web3.js');
const { Connection, PublicKey, LAMPORTS_PER_SOL, clusterApiUrl } = SOLANA;
const SOLANA_CONNECTION = new Connection(clusterApiUrl('devnet'));
const WALLET_ADDRESS = '9HekP9CfByCcDrfneqNR7BPgsNYob2woRaN3WqqS9tKP'; //👈 Replace with your wallet address
const AIRDROP_AMOUNT = 1 * LAMPORTS_PER_SOL; // 1 SOL 

(async () => {
    console.log(`Requesting airdrop for ${WALLET_ADDRESS}`)
    const signature = await SOLANA_CONNECTION.requestAirdrop(
        new PublicKey(WALLET_ADDRESS),
        AIRDROP_AMOUNT
    );
    const { blockhash, lastValidBlockHeight } = await SOLANA_CONNECTION.getLatestBlockhash();
    await SOLANA_CONNECTION.confirmTransaction({
        blockhash,
        lastValidBlockHeight,
        signature
    },'finalized');
    console.log(`Tx Complete: https://explorer.solana.com/tx/${signature}?cluster=devnet`)
})();
```


## Execute Smart contract

1. cargo build-bpf  < this generate a file with extension .so
2. solana program deploy program.so  < what is a contract is a certly work 
3. Error if you don't has funds > Error: Account 4bWiPgCsTdbgtu3WZokG9rh5gVUQpPHFDVLVPd3Eq45U has insufficient funds for spend (0.48122136 SOL) + fee (0.00036 SOL)


## OWASP TOP 10 Smart contract

- SC01:2023 - Reentrancy Attacks
- SC02:2023 - Integer Overflow and Underflow
- SC03:2023 - Timestamp Dependence
- SC04:2023 - Access Control Vulnerabilities
- SC05:2023 - Front-running Attacks
- SC06:2023 - Denial of Service (DoS) Attacks
- SC07:2023 - Logic Errors
- SC08:2023 - Insecure Randomness
- SC09:2023 - Gas Limit Vulnerabilities
- SC10:2023 - Unchecked External Calls
