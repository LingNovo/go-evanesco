## Evanesco Main Chain

The goal of Evanesco Main Chain is to bring programmability and interoperability to Evanesco Ecology. In order to embrace the existing popular community and advanced technology, it will bring huge benefits by staying compatible with all the existing smart contracts on Ethereum and Ethereum tooling. And to achieve that, the easiest solution is to develop based on go-ethereum fork, as we respect the great work of Ethereum very much.

Evanesco Main Chain starts its development based on go-ethereum fork. So you may see many toolings, binaries and also docs are based on Ethereum ones.

[![API Reference](
https://camo.githubusercontent.com/915b7be44ada53c290eb157634330494ebe3e30a/68747470733a2f2f676f646f632e6f72672f6769746875622e636f6d2f676f6c616e672f6764646f3f7374617475732e737667
)](https://pkg.go.dev/github.com/ethereum/go-ethereum?tab=doc)
[![Discord](https://img.shields.io/badge/discord-join%20chat-blue.svg)](https://discord.com/invite/VnYXBSF)

**The Evanesco Main Chain** will be:

- **A self-sovereign blockchain**: Provides security and safety with miner and elected validators.
- **EVM-compatible**: Supports all the existing Ethereum tooling along with faster finality and cheaper transaction fees.
- **Interoperable**: Comes with efficient native dual chain communication; Optimized for scaling high-performance dApps that require fast and smooth user experience.
- **Distributed with on-chain governance**: GPOW brings in decentralization and community participants. As the native token, EVA will serve as both the gas of smart contract execution and tokens for staking.

Cross-chain transfer and other communication are possible due to native support of interoperability. CrossWrapper and on-chain contracts are developed to support that. 

More details in [White Paper](https://evanesco.org/assets/whitepaper.pdf).

## Key features

### Grandpa over PoW
Although Proof-of-Work (PoW) has been approved as a practical mechanism to implement a decentralized network, it is not friendly to the environment and also requires a large size of participants to maintain the security and consistency.

To combine PoW and Grandpa for consensus, Evanesco Main Chain implement a novel consensus engine called GPoW that:

GPoW consensus includes two layers of consensus mechanisms, which are nested, influence each other and play different roles. GPoW algorithm not only provides almost real-time, asynchronous and safe finality similar to GRANDPA algorithm, but also can fairly distribute new tokens according to PoW, enabling a wider range of communities to go in for the construction of the whole ecology.
The basic steps of the GPoW consensus are:
1.	When the whole network starts, the network miners start to run PoW algorithm and transmit data based on the privacy cascade communication protocol.
a.In the case of transaction or routing data, public or cascaded private transmission is set based on transaction settings
b.In the case of a PoW block, it is publicly broadcast to nearby network nodes
c.On average, the network miner calculates a PoW block and broadcasts it every 10 minutes

2.	The two-layer Sorter network packages the broadcast transactions into blocks, and determines the final consistency of the whole chain according to GRANDPA protocol.
a.In the case of transaction data, the block-generating person is obtained according to the drawing algorithm, and the block is generated and determined as final (second level)
b.In the case of a PoW block, the most suitable block is determined according to the content of the block broadcast by the block-generating person and the finality is determined (10 minutes)


Now we are at the stage of **α-testnet**, Evanesco α Chain introduces a system of 7 validators with POA consensus that can support Privacy Account and EVM-compatible privacy-middleware. It is very easy to test the functionality of Evanesco.


## Native Token

EVA will run on Evanesco Main Chain in the same way as ETH runs on Ethereum so that it remains as `native token` for Evanesco. This means,
EVA will be used to:

1. pay `gas` to deploy or invoke Smart Contract on Evanesco Main Chain
2. perform cross-chain operations, such as transfer token assets across Evanesco Main Chain and Ethereum.

## Building the source

Many of the below are the same as or similar to go-ethereum.

For prerequisites and detailed build instructions please read the [Installation Instructions](https://geth.ethereum.org/docs/install-and-build/installing-geth).

Building `eva` requires both a Go (version 1.14 or later) and a C compiler. You can install
them using your favourite package manager. Once the dependencies are installed, run

```shell
make eva
```

or, to build the full suite of utilities:

```shell
make all
```

## Executables

The evanesco project comes with several wrappers/executables found in the `cmd`
directory.

|    Command    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| :-----------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  **`eva`**   | Evanesco Main Chain client binary. It is the entry point into the Evanesco network (main-, test- or private net), capable of running as a full node (default), archive node (retaining all historical state) or a light node (retrieving data live). It has the same and more RPC and other interface as go-ethereum and can be used by other processes as a gateway into the Evanesco network via JSON RPC endpoints exposed on top of HTTP, WebSocket and/or IPC transports. `eva --help` and the [CLI page](https://geth.ethereum.org/docs/interface/command-line-options) for command line options.          |
|   `clef`      | Stand-alone signing tool, which can be used as a backend signer for `eva`.  |
|   `devp2p`    | Utilities to interact with nodes on the networking layer, without running a full blockchain. |
|   `abigen`    | Source code generator to convert Ethereum contract definitions into easy to use, compile-time type-safe Go packages. It operates on plain [Ethereum contract ABIs](https://docs.soliditylang.org/en/develop/abi-spec.html) with expanded functionality if the contract bytecode is also available. However, it also accepts Solidity source files, making development much more streamlined. 
|  `bootnode`   | Stripped down version of our Ethereum client implementation that only takes part in the network node discovery protocol, but does not run any of the higher level application protocols. It can be used as a lightweight bootstrap node to aid in finding peers in private networks.                                                                                                                                                                                                                                                                 |
|     `evm`     | Developer utility version of the EVM (Ethereum Virtual Machine) that is capable of running bytecode snippets within a configurable environment and execution mode. Its purpose is to allow isolated, fine-grained debugging of EVM opcodes (e.g. `evm --code 60ff60ff --debug run`).                                                                                                                                                                                                                                                                     |
|   `rlpdump`   | Developer utility tool to convert binary RLP ([Recursive Length Prefix](https://eth.wiki/en/fundamentals/rlp)) dumps (data encoding used by the Ethereum protocol both network as well as consensus wise) to user-friendlier hierarchical representation (e.g. `rlpdump --hex CE0183FFFFFFC4C304050583616263`).                                                                                                                                                                                                                                 |

## Running `eva`

Going through all the possible command line flags is out of scope here,
but we've enumerated a few common parameter combos to get you up to speed quickly
on how you can run your own `eva` instance.

### Hardware Requirements

The hardware must meet certain requirements to run a full node.
- VPS running recent versions of Mac OS X or Linux.
- 1T of SSD storage for mainnet, 500G of SSD storage for testnet.
- 8 cores of CPU and 32 gigabytes of memory (RAM) for mainnet.
- 4 cores of CPU and 8 gigabytes of memory (RAM) for testnet.
- A broadband Internet connection with upload/download speeds of at least 10 megabyte per second

```shell
$ eva console
```

This command will:
* Start `eva` in fast sync mode (default, can be changed with the `--syncmode` flag),
  causing it to download more data in exchange for avoiding processing the entire history
  of the Evanesco Main Chain network, which is very CPU intensive.
* Start up `eva`'s built-in interactive, just as ethereum tool geth: [JavaScript console](https://geth.ethereum.org/docs/interface/javascript-console),
  (via the trailing `console` subcommand) through which you can interact using [`web3` methods](https://web3js.readthedocs.io/en/)
  This tool is optional and if you leave it out you can always attach to an already running
  `eva` instance with `eva attach`.

### A Full node on the α test network

TBD

### Configuration

As an alternative to passing the numerous flags to the `eva` binary, you can also pass a
configuration file via:

```shell
$ eva --config /path/to/your_config.toml
```

To get an idea how the file should look like you can use the `dumpconfig` subcommand to
export your existing configuration:

```shell
$ eva --your-favourite-flags dumpconfig
```

### Programmatically interfacing `eva` nodes

As a developer, sooner rather than later you'll want to start interacting with `eva` and the
Evanesco network via your own programs and not manually through the console. To aid
this, `eva` has built-in support for a JSON-RPC based APIs, as on Ethereum, ([standard APIs](https://eth.wiki/json-rpc/API))

These can be exposed via HTTP, WebSockets and IPC (UNIX sockets on UNIX based
platforms, and named pipes on Windows).

The IPC interface is enabled by default and exposes all the APIs supported by `eva`,
whereas the HTTP and WS interfaces need to manually be enabled and only expose a
subset of APIs due to security reasons. These can be turned on/off and configured as
you'd expect.

HTTP based JSON-RPC API options:

* `--http` Enable the HTTP-RPC server
* `--http.addr` HTTP-RPC server listening interface (default: `localhost`)
* `--http.port` HTTP-RPC server listening port (default: `8545`)
* `--http.api` API's offered over the HTTP-RPC interface (default: `eth,net,web3`)
* `--http.corsdomain` Comma separated list of domains from which to accept cross origin requests (browser enforced)
* `--ws` Enable the WS-RPC server
* `--ws.addr` WS-RPC server listening interface (default: `localhost`)
* `--ws.port` WS-RPC server listening port (default: `8546`)
* `--ws.api` API's offered over the WS-RPC interface (default: `eth,net,web3`)
* `--ws.origins` Origins from which to accept websockets requests
* `--ipcdisable` Disable the IPC-RPC server
* `--ipcapi` API's offered over the IPC-RPC interface (default: `admin,debug,eth,miner,net,personal,shh,txpool,web3`)
* `--ipcpath` Filename for IPC socket/pipe within the datadir (explicit paths escape it)

You'll need to use your own programming environments' capabilities (libraries, tools, etc) to
connect via HTTP, WS or IPC to a `eva` node configured with the above flags and you'll
need to speak [JSON-RPC](https://www.jsonrpc.org/specification) on all transports. You
can reuse the same connection for multiple requests!

**Note: Please understand the security implications of opening up an HTTP/WS based
transport before doing so! Hackers on the internet are actively trying to subvert
Evanesco Main Chain nodes with exposed APIs! Further, all browser tabs can access locally
running web servers, so malicious web pages could try to subvert locally available
APIs!**

## Contribution

Thank you for considering to help out with the source code! We welcome contributions
from anyone on the internet, and are grateful for even the smallest of fixes!

If you'd like to contribute to evanesco, please fork, fix, commit and send a pull request
for the maintainers to review and merge into the main code base. If you wish to submit
more complex changes though, please check up with the core devs first on [our discord channel](https://discord.com/invite/VnYXBSF)
to ensure those changes are in line with the general philosophy of the project and/or get
some early feedback which can make both your efforts much lighter as well as our review
and merge procedures quick and simple.

Please make sure your contributions adhere to our coding guidelines:

* Code must adhere to the official Go [formatting](https://golang.org/doc/effective_go.html#formatting)
  guidelines (i.e. uses [gofmt](https://golang.org/cmd/gofmt/)).
* Code must be documented adhering to the official Go [commentary](https://golang.org/doc/effective_go.html#commentary)
  guidelines.
* Pull requests need to be based on and opened against the `master` branch.
* Commit messages should be prefixed with the package(s) they modify.
    * E.g. "eth, rpc: make trace configs optional"


## License

The evanesco library (i.e. all code outside of the `cmd` directory) is licensed under the
[GNU Lesser General Public License v3.0](https://www.gnu.org/licenses/lgpl-3.0.en.html),
also included in our repository in the `COPYING.LESSER` file.

The evanesco binaries (i.e. all code inside of the `cmd` directory) is licensed under the
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html), also
included in our repository in the `COPYING` file.
