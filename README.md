# Soroban Vault

**Important**: This is a draft implementation intended for testing purposes only. For production deployments, we strongly recommend using [OpenZeppelin's audited standard contracts](https://github.com/OpenZeppelin/stellar-contracts).

---

First and foremost, setup development environment:

https://developers.stellar.org/docs/build/smart-contracts/getting-started/setup

VS Code Extension: https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer

---

Identity (address):

```
stellar keys generate --global bob --network testnet --fund

stellar keys address bob

stellar keys show bob
```

Contract:

```
cd soroban-4626

stellar contract build

stellar contract optimize --wasm target/wasm32v1-none/release/vault.wasm

stellar contract deploy \
  --wasm target/wasm32v1-none/release/vault.wasm \
  --source bob \
  --network testnet

// Copy-paste deployed contract address, bob's (or similar) address and underlying asset address:

Sample: https://lab.stellar.org/r/testnet/contract/CA7BZCDSB2AYTFMCP3ABYU3JFN3MC7MRKZ2KY5EY6UUHR37OSRDV3L67

stellar contract invoke --id <contract_address> --source bob --network testnet -- initialize --admin <admin_address> --asset_address <asset_address>


stellar contract invoke --id CA7BZCDSB2AYTFMCP3ABYU3JFN3MC7MRKZ2KY5EY6UUHR37OSRDV3L67 --source bob --network testnet -- initialize --admin bob --asset_address CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA --lock_timestamp 86000 --unlock_timestamp 604800



[Market Maker Commands](COMMANDS.md)

---

USDC asset example:

https://www.circle.com/multi-chain-usdc/stellar

Testnet contract address: CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA

Mainnet contract address: CCW67TSZV3SSS2HXMBQ5JFGCKJNXKZM7UQUWUZPUTHXSTZLEO7SJMI75

---

Query asset contract IDs:

```
// Testnet USDC
stellar contract id asset --network testnet --asset USDC:GBBD47IF6LWK7P7MDEVSCWR7DPUWV3NY3DTQEVFL4NAT4AQH3ZLLFLA5
// CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA

// Mainnet USDC
stellar contract id asset --network mainnet --asset USDC:GA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN
// CCW67TSZV3SSS2HXMBQ5JFGCKJNXKZM7UQUWUZPUTHXSTZLEO7SJMI75

// Testnet XLM
stellar contract id asset --network testnet --asset native
// CDLZFC3SYJYDZT7K67VZ75HPJVIEUVNIXF47ZG2FB2RMQQVU2HHGCYSC

// Mainnet XLM
stellar contract id asset --network mainnet --asset native
// CAS3J7GYLGXMF6TDJBBYYSE3HQ6BBSMLNUQ34T6TZMYMW2EVH34XOWMA
```

---

Token Interface:

https://developers.stellar.org/docs/tokens/token-interface

```
pub trait TokenInterface
```

(SAC) Stellar Asset Contract:

https://developers.stellar.org/docs/tokens/stellar-asset-contract

https://developers.stellar.org/docs/build/guides/tokens

```
pub trait StellarAssetInterface
```

---

> [!Warning]
> While we strive to ensure this software functions as intended, it is provided “as is” with no warranties or guarantees of any kind. Smart contracts are inherently complex and may contain bugs, vulnerabilities, or unintended behaviors. By using this software, you acknowledge and agree that: You use it entirely at your own risk. You should perform your own due diligence, and it is strongly recommended to consult qualified professionals (e.g., security auditors, legal advisors). We do not accept any liability for any loss of funds, damages, or other consequences resulting from the use or misuse of this code.
