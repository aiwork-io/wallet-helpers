# Wallet Helpers
This repo contains the code and set-up instructions of the wallet helper which verifies the awo transaction between the wallet of the user procuring AI resources and the the marketplace wallet

## How to deploy

1. Copy `.env.example` to `.env` and replace default configs with your configs.
2. Create your docker image `docker build -t kubeplusplus/wallet-helpers .`
3. Run the container `docker run -p 3000:3000 kubeplusplus/wallet-helpers` and use some commands bellow to test

## How to use

### With ECR20 Token

```bash
# Transfer
curl -X POST \
    -H "Content-Type: application/json" \
    -H "AuthToken: VtufbvX3QpGJvmTaKTvB97LqX0RDCTrcuJFQ2GM4WYGKykK69GnuMTg1lP1J0zEJ" \
    -d '{"recipient_wallet":"0xA7E9eDbD4d311613963764BD65870c863967A92a","amount":128}' \
    http://127.0.0.1:3000/transfer

{"blockHash":"0x293732e1b237b01285b7fbae5d062991f6496ad1a335cf731bc7d511e980c113","blockNumber":13879069,"contractAddress":null,"cumulativeGasUsed":4738365,"from":"0x0eed72b06a3737ac6d88cee445c6b716027b84c3","gasUsed":36284,"logsBloom":"0x00000000000008000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000200000000000000200000000000000000000000000000000000000000000010000000000000100000000000000000000000000000001000000000040000000000000000000000000000000000080000000000000000000000000000000040000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","status":true,"to":"0xa1daa25016d83895f215ee724c78fcc1085accb2","transactionHash":"0x9bc4b82b0f1065597dcdc0208ac775b68013e0e841d70d4274a0a04932bc9864","transactionIndex":4,"type":"0x0","events":{"Transfer":{"address":"0xa1DaA25016D83895f215eE724c78fcC1085aCCb2","blockNumber":13879069,"transactionHash":"0x9bc4b82b0f1065597dcdc0208ac775b68013e0e841d70d4274a0a04932bc9864","transactionIndex":4,"blockHash":"0x293732e1b237b01285b7fbae5d062991f6496ad1a335cf731bc7d511e980c113","logIndex":21,"removed":false,"id":"log_8e02d3de","returnValues":{"0":"0x0EED72B06a3737aC6D88CEE445c6b716027b84c3","1":"0xA7E9eDbD4d311613963764BD65870c863967A92a","2":"128000000000000000000","from":"0x0EED72B06a3737aC6D88CEE445c6b716027b84c3","to":"0xA7E9eDbD4d311613963764BD65870c863967A92a","value":"128000000000000000000"},"event":"Transfer","signature":"0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef","raw":{"data":"0x000000000000000000000000000000000000000000000006f05b59d3b2000000","topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef","0x0000000000000000000000000eed72b06a3737ac6d88cee445c6b716027b84c3","0x000000000000000000000000a7e9edbd4d311613963764bd65870c863967a92a"]}}}}

# Check
curl -H "AuthToken: VtufbvX3QpGJvmTaKTvB97LqX0RDCTrcuJFQ2GM4WYGKykK69GnuMTg1lP1J0zEJ" \
    http://127.0.0.1:3000/check?wallet_id=0xA7E9eDbD4d311613963764BD65870c863967A92a&from_wallet_id=0x0eed72b06a3737ac6d88cee445c6b716027b84c3&transaction_id=0x9bc4b82b0f1065597dcdc0208ac775b68013e0e841d70d4274a0a04932bc9864&amount=128

{"ok":true}
```

### With BNB

```bash
# Transfer
curl -X POST \
    -H "Content-Type: application/json" \
    -H "AuthToken: VtufbvX3QpGJvmTaKTvB97LqX0RDCTrcuJFQ2GM4WYGKykK69GnuMTg1lP1J0zEJ" \
    -d '{"recipient_wallet":"0xA7E9eDbD4d311613963764BD65870c863967A92a","amount":0.01}' \
    http://127.0.0.1:3000/transfer?currency=bnb

{"blockHash":"0xd084032b5f2a8b50ddbb68f7269be96374261f9c76a04f289d7482aec041822b","blockNumber":13879161,"contractAddress":null,"cumulativeGasUsed":7289248,"from":"0x0eed72b06a3737ac6d88cee445c6b716027b84c3","gasUsed":21000,"logs":[],"logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","status":true,"to":"0xa7e9edbd4d311613963764bd65870c863967a92a","transactionHash":"0x15c7123e60e3e9b6670945673ed045a041bdc4ccadf2d35957346c47183a816b","transactionIndex":4,"type":"0x0"}

# Check
curl -H "AuthToken: VtufbvX3QpGJvmTaKTvB97LqX0RDCTrcuJFQ2GM4WYGKykK69GnuMTg1lP1J0zEJ" \
    http://127.0.0.1:3000/check?wallet_id=0xA7E9eDbD4d311613963764BD65870c863967A92a&from_wallet_id=0x0eed72b06a3737ac6d88cee445c6b716027b84c3&transaction_id=0x15c7123e60e3e9b6670945673ed045a041bdc4ccadf2d35957346c47183a816b&amount=0.01

{"ok":true}
```

### With Eth

```
curl -H "AuthToken: VtufbvX3QpGJvmTaKTvB97LqX0RDCTrcuJFQ2GM4WYGKykK69GnuMTg1lP1J0zEJ" \
    http://127.0.0.1:3000/check?wallet_id=0xaff015ae8fb7df94898c1c86440321e9352157e9&from_wallet_id=0x81e7eebf0f243053b52096b1a328f64dc6abbe59&transaction_id=0x532099685e662846dac240cc1428421866b62e587aa05ce8b8e5b10524e6f1dc&amount=0.0001
{"ok":true}
```
