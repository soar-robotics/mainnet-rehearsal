
# Instructions for Validators

## Upgrade Go Version

### Update Go to Version 1.22.3:

```sh
wget https://golang.org/dl/go1.22.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
```

### Verify Go Version:

```sh
go version
# Output should be: go version go1.22.3 linux/amd64
```

## Update WasmVM Library

### Download the new libwasmvm.x86_64.so:

```sh
wget https://github.com/CosmWasm/wasmvm/releases/download/v1.5.2/libwasmvm.x86_64.so
```

### Move the library to the appropriate directory:

```sh
sudo mv libwasmvm.x86_64.so /usr/lib/
# OR
sudo mv libwasmvm.x86_64.so /usr/local/lib/
```

## Initialize the Node

### Initialize the node:

```sh
soarchaind init --nodeName --chain-id soarchaintestnet --default-denom utsoar
```

### Configure the Testnet Validator Account:

```sh
soarchaind config set client chain-id soarchaintestnet
soarchaind config set client keyring-backend test
soarchaind keys add keyName --keyring-backend test --algo secp256k1 --recover
```

### Replace the Genesis File:

Replace the binary with `pregenesis.json`. Your `genesis.json` is in the `.soarchain/config` directory. The file name should remain `genesis.json`.

## Create Gentx:

```sh
soarchaind genesis gentx keyName 1000000utsoar --keyring-backend test --chain-id soarchaintestnet
```

After completing these steps, validators can start sending their gentx files.

For more information on the WasmVM upgrade, refer to the [WasmVM v1.5.2 release](https://github.com/CosmWasm/wasmvm/releases/tag/v1.5.2).

We appreciate your cooperation in ensuring a smooth mainnet launch process. Please refactor and verify all files as needed.

Make sure to replace `--nodeName` and `keyName` with the actual names you intend to use.

For any questions, we are here in our social media groups.

Thank you,  
The Soarchain Team
