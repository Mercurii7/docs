# Configuring and Starting Neo-CLI 

After installation of Neo-CLI, this section we will walk you through the necessary configurations before running Neo-CLI and the steps to start Neo-CLI using commands. 

## Modifying configuration files

Neo-CLI accesses the configuration file `config.json`  during execution. You need to make necessary configurations in the file before starting Neo-CLI.

### Configuring a wallet

To make Neo-CLI automatically open a wallet when running, you can configure the wallet in  `config.json`  beforehand, as follows:

- `Path`: the wallet path
- `Password`: the wallet password. Note that the password configured here is displayed in plaintext!
- `IsActive`: Set to `true` to allow Neo-CLI to open the wallet automatically.

Here is an example:

```json
{
  "ApplicationConfiguration": {
    "Logger": {
      "Path": "Logs",
      "ConsoleOutput": false,
      "Active": false
    },
    "Storage": {
      "Engine": "LevelDBStore",
      "Path": "Data_LevelDB_{0}"
    },
    "P2P": {
      "Port": 10333,
      "WsPort": 10334
    },
    "UnlockWallet": {
      "Path": "wallet.json",
      "Password": "1",
      "IsActive": true
    },
    "PluginURL": "https://github.com/neo-project/neo-modules/releases/download/v{1}/{0}.zip"
  },
  "ProtocolConfiguration": {
    "Network": 860833102,
    "AddressVersion": 53,
    "MillisecondsPerBlock": 15000,
    "MaxTransactionsPerBlock": 512,
    "MemoryPoolMaxTransactions": 50000,
    "MaxTraceableBlocks": 2102400,
    "InitialGasDistribution": 5200000000000000,
    "ValidatorsCount": 7,
    "StandbyCommittee": [
      "03b209fd4f53a7170ea4444e0cb0a6bb6a53c2bd016926989cf85f9b0fba17a70c",
      "02df48f60e8f3e01c48ff40b9b7f1310d7a8b2a193188befe1c2e3df740e895093",
      "03b8d9d5771d8f513aa0869b9cc8d50986403b78c6da36890638c3d46a5adce04a",
      "02ca0e27697b9c248f6f16e085fd0061e26f44da85b58ee835c110caa5ec3ba554",
      "024c7b7fb6c310fccf1ba33b082519d82964ea93868d676662d4a59ad548df0e7d",
      "02aaec38470f6aad0042c6e877cfd8087d2676b0f516fddd362801b9bd3936399e",
      "02486fd15702c4490a26703112a5cc1d0923fd697a33406bd5a1c00e0013b09a70",
      "023a36c72844610b4d34d1968662424011bf783ca9d984efa19a20babf5582f3fe",
      "03708b860c1de5d87f5b151a12c2a99feebd2e8b315ee8e7cf8aa19692a9e18379",
      "03c6aa6e12638b36e88adc1ccdceac4db9929575c3e03576c617c49cce7114a050",
      "03204223f8c86b8cd5c89ef12e4f0dbb314172e9241e30c9ef2293790793537cf0",
      "02a62c915cf19c7f19a50ec217e79fac2439bbaad658493de0c7d8ffa92ab0aa62",
      "03409f31f0d66bdc2f70a9730b66fe186658f84a8018204db01c106edc36553cd0",
      "0288342b141c30dc8ffcde0204929bb46aed5756b41ef4a56778d15ada8f0c6654",
      "020f2887f41474cfeb11fd262e982051c1541418137c02a0f4961af911045de639",
      "0222038884bbd1d8ff109ed3bdef3542e768eef76c1247aea8bc8171f532928c30",
      "03d281b42002647f0113f36c7b8efb30db66078dfaaa9ab3ff76d043a98d512fde",
      "02504acbc1f4b3bdad1d86d6e1a08603771db135a73e61c9d565ae06a1938cd2ad",
      "0226933336f1b75baa42d42b71d9091508b638046d19abd67f4e119bf64a7cfb4d",
      "03cdcea66032b82f5c30450e381e5295cae85c5e6943af716cc6b646352a6067dc",
      "02cd5a5547119e24feaa7c2a0f37b8c9366216bab7054de0065c9be42084003c8a"
    ],
    "SeedList": [
      "seed1.neo.org:10333",
      "seed2.neo.org:10333",
      "seed3.neo.org:10333",
      "seed4.neo.org:10333",
      "seed5.neo.org:10333"
    ]
  }
}
```

Where:

- `ConsoleOutput`: Whether to print log information on console. `true` means foreground and background printing, while `false` means background logging.
- `Active`: Whether to enable Log
- `Engine`: It defaults to LevelDBStore, which means the engine used by the blockchain to store data.
- `PluginURL`: The downloading URL of the plugin, which will be used when using the CLI install command.

### Connecting the node to network

Neo-CLI connects to N3 main net by default. To connect the node to test net, replace the content of `config.json` with the content of  `config.testnet.json`. 

To connect the node to your private net, refer to [Setting up Private Chain](../../develop/network/private-chain/solo.md).

## Installing plugins

Some additional functionalities are individually encapsulated in plug-ins for the purpose of improving node security, stability, and flexibility. The user can select the desired extension functionality instead of invoking it with additional parameters every time starting neo-cli, thus avoiding many human errors and some tedious instructions such as opening a wallet and calling APIs. 

You can choose one of the following ways to install plugins:

- Download the plugin package from GitHub
- Use the CLI command to install automatically

### Downloading plugins from GitHub

Download the plugins you need from the following table.

<table class="table table-hover">
    <thead>
        <tr>
            <th style="width: 25%;">Plugin</th>
            <th style="width: 35%;">Description</th>
            <th style="width: 20%;">API Included</th>
            <th style="width: 20%;"></th>
        </tr>
    </thead>
    <tbody>
            <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/ApplicationLogs.zip">ApplicationLogs</a>
            </td>
            <td>Synchronizes the smart contract log with the NativeContract log (Notify)</td>
            <td><a href="../../reference/rpc/latest-version/api/getapplicationlog.html">getapplicationlog</a></td>
            <td>Recommended</td>
        </tr>
          <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/DBFTPlugin.zip">DBFTPlugin</a>
            </td>
            <td>dBFT consensus plugin</td>
            <td></td>
            <td>Mandatory when served as a consensus node</td>
        </tr>   
        <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/LevelDBStore.zip">LevelDBStore</a>
            </td>
            <td>Uses LevelDB to store the blockchain data</td>
            <td></td>    
            <td>Mandatory</td>
        </tr>
             <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/OracleService.zip">OracleService</a>
            </td>
            <td>Oracle service plugin</td>
            <td></td>
            <td>Mandatory when served as an Oracle node</td>
        </tr>
        <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/RocksDBStore.zip">RocksDBStore</a>
            </td>
            <td>Uses RocksDBStore to store the blockchain data</td>
            <td></td>
            <td>An alternative to LevelDBStore</td>
        </tr>
                <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/RpcNep17Tracker.zip">RpcNep17Tracker</a>
            </td>
            <td>Enquiries NEP17 balance and transactions history of accounts through RPC</td>
            <td><a href="../../reference/rpc/latest-version/api/getnep17balances.html">getnep17balances</a><br><a
                    href="../../reference/rpc/latest-version/api/getnep17transfers.html">getnep17transfers</a></td>
            <td>Recommended</td>
        </tr>
        <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/RpcServer.zip">RpcServer</a>
            </td>
            <td>Enables RPC for the node</td>
            <td><a href="../../reference/rpc/latest-version/api.html"> RPC API </a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/StatesDumper.zip">StatesDumper</a>
            </td>
            <td>Exports Neo-CLI status data.</td>
            <td></td>
            <td>Optional</td>
        </tr>  
         <tr>
            <td><a
                    href="https://github.com/neo-project/neo-modules/releases/download/v3.0.1/StateService.zip">StateService</a>
            </td>
            <td>StateRoot consensus service plugin</td>
            <td><a href="../../reference/rpc/latest-version/api/getstateroot.html">getstateroot</a><br>
                <a href="../../reference/rpc/latest-version/api/getproof.html">getproof</a><br>
                <a href="../../reference/rpc/latest-version/api/verifyproof.html">verifyproof</a><br>
                <a href="../../reference/rpc/latest-version/api/getstateheight.html">getstateheight</a>
            </td>
            <td>Mandatory when served as a StateRoot consensus node</td>
        </tr>   
    </tbody>
</table>




![](../../../zh-cn/assets/PluginsForExchange.png)

### Downloading plugins using command

It is easier to automatically install or uninstall the plugin using commands, for example:

```
neo> install StatesDumper
Downloading from https://github.com/neo-project/neo-modules/releases/download/v3.0.1/StatesDumper.zip
Install successful, please restart neo-cli.
```

```
neo> uninstall StatesDumper
Uninstall successful, please restart neo-cli.
```

After installation, restart Neo-CLI for the plugin to take effect.

## Starting the NEO node

Open the command line, navigate to the Neo-CLI directory, and enter the following command to start the Neo node:

On **Windows 10**:

```
dotnet neo-cli.dll
```

or 

```
neo-cli.exe
```

On **Linux (ubuntu 16.04/18.04)**:

```
./neo-cli
```

or

```
dotnet neo-cli.dll
```

> [!Note]
>
> If you  use dotnet install .net core in advance.

If you want the external program to access the node API need to open the firewall port: 10331-10334, 20331-20334

> [!WARNING]
>
> If you open the API service and the wallet in Neo-CLI, you need to set up your firewall policy. For example, set a whitelist for the firewall to only allow access to these ports by whitelisted IP addresses. If completely opening the service to external network, others may be able to export the private key or transfer assets using API.