Ethereum Network Intelligence API
=================================

This is the backend service which runs along with ethereum nodes and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to an [ethstats-server](https://github.com/goerli/ethstats-server) to feed information.

## Available dashboards
* https://ethstats.net
* https://stats.goerli.net
* https://kotti.goerli.net
* https://mordor.dash.fault.dev
* https://classic.dash.fault.dev

## Prerequisite
* client: geth, besu, nethermind, or openethereum
* reporting: node js, npm, and pm2

## Installation

Clone the repository, install node dependencies, and run the pm2 daemon.

```bash
git clone https://github.com/Opulent-X/ethstats-client.git
cd ethstats-client/
npm install
sudo npm install -g pm2
```

## Configuration

Configure the app modifying [app.json](/app.json). 

```json
[
  {
    "name"              : "besu-goerli",
    "script"            : "app.js",
    "log_date_format"   : "YYYY-MM-DD HH:mm Z",
    "merge_logs"        : false,
    "watch"             : false,
    "max_restarts"      : 10,
    "exec_interpreter"  : "node",
    "exec_mode"         : "fork_mode",
   
  }
]
```
And also this the environment file (.env)

```config
RPC_HOST=localhost
RPC_PORT=8545
LISTENING_PORT=30303
INSTANCE_NAME=BETA Connect Node
CONTACT_DETAILS=beta@opulent-x.com
WS_SERVER=ws://localhost:3030
WS_SECRET=beta-net-stats-has-a-secret
VERBOSITY= 2
```

Ask in Gitter for the secret: https://gitter.im/goerli/testnet

Available Websockets:
* `ws://ethstats.net:3000`
* `ws://stats.goerli.net:3000`
* `ws://kotti.goerli.net:3000`
* `ws://mordor.dash.fault.dev:3000`
* `ws://classic.dash.fault.dev:3000`

The secrets for Mordor, Kotti, Goerli, and Classic are the same. The Ethereum mainnet secret is different.

## Run

Run it using pm2:

```bash
pm2 start app.json
```
