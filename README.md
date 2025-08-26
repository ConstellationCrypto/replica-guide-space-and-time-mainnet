Please reach out to the team for the mainnet guide. This is the testnet guide for now and will be upgraded upon request. Testnet guide can also be found here: 
https://github.com/ConstellationCrypto/replica-guide-space-and-time-testnet

# Replica Guide

To use: You'll want to bring your own more performant RPC URL for the base chain instead of using the default. Configure this via the `EN_ETH_CLIENT_URL` environment variable in the `external-node` service in `docker-compose.yml`. Then run `docker compose up`.

A number of constants have already been set:

- the chain IDs for L1 (`EN_L1_CHAIN_ID: 11155111` which is sepolia) and L2 (`EN_L2_CHAIN_ID: 19110` which is the SxT testnet)
- the sequencer http url (`EN_MAIN_NODE_URL: https://sxt-testnet.rpc.caldera.xyz/http`), which allows for transactions sent to the replica node to be forwarded to the sequencer, effectively meaning you can use the replica node like a full RPC provider

The RPC is exposed via port 3060 (HTTP) and 3061 (websocket) as specified in the `docker-compose.yml`. After running `docker compose up`, you may query the RPC as follows:

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"jsonrpc":"2.0","id":0,"method":"eth_chainId","params":[]}' \
localhost:3060

{"jsonrpc":"2.0","result":"0x4aa6","id":0}
```

- The `docker-compose.yml` also includes services for prometheus and grafana, but these aren't necessary to spin up
- The postgres user password should probably be changed from the default value (`POSTGRES_PASSWORD` env variable)

