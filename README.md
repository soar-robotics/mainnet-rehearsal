
# Instructions for Validators

Validators testnet accounts have been reserved in pregenesis.json 

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
## Replace or add the new binary 

First clone the mainnet-rehearsal repository 
```sh
cd $HOME
git clone https://github.com/soar-robotics/mainnet-rehearsal.git 
```
Move the binary for system usage 
```sh
cd mainnet-rehearsal/binary
tar -xvf soarchaind.tar.gz
sudo mv soarchaind /usr/local/go/bin
```

## Initialize the Node

### Initialize the node:

```sh
soarchaind init <nodeName> --chain-id soarchaintestnet --default-denom utsoar
```

### Configure the Testnet Validator Account:

```sh
soarchaind config set client chain-id soarchaintestnet
soarchaind config set client keyring-backend test
soarchaind keys add <keyName> --keyring-backend test --algo secp256k1 --recover
```

### Replace the Genesis File:

Replace the binary with `pregenesis.json`. Your `genesis.json` is in the `.soarchain/config` directory. The file name should remain `genesis.json`.

## Create Gentx:

```sh
soarchaind genesis gentx <keyName> 1000000utsoar --keyring-backend test --chain-id soarchaintestnet
```

After completing these steps, validators can start sending their gentx files.


# Instructions for Sending `gentx` Pull Requests

## Fork the Repository

1. Go to the [repository](https://github.com/soar-robotics/mainnet-rehearsal) and click the "Fork" button in the upper right corner to create a copy of the repository in your GitHub account.

## Clone Your Forked Repository

2. Open your terminal and run:
   ```sh
   git clone git@github.com:soar-robotics/mainnet-rehearsal.git
   cd mainnet-rehearsal
   ```

## Create a New Branch

3. Create a new branch for your `gentx` file:
   ```sh
   git checkout -b add-gentx-<your-validator-name>
   ```

## Add Your `gentx` File

4. Copy your `gentx` file to the `gentx` directory in the repository. Make sure to name the file `gentx-<your-validator-name>.json`:
   ```sh
   cp $HOME/.soarchain/config/gentx/gentx.json network/gentxs/gentx-<your-validator-name>.json
   ```

## Commit Your Changes

5. Commit your changes with a descriptive message:
   ```sh
   git add network/gentxs/gentx-<your-validator-name>.json
   git commit -m "Add gentx for <your-validator-name>"
   ```

## Push Your Branch to GitHub

6. Push your branch to your forked repository:
   ```sh
   git push origin add-gentx-<your-validator-name>
   ```

## Create a Pull Request

7. Go to your forked repository on GitHub.
   - Click the "Compare & pull request" button.
   - Add a descriptive title and comment for your pull request, then click "Create pull request".


```markdown
## Description

Add `gentx` for <your-validator-name>

## Checklist

- [ ] Updated `gentx` directory with my `gentx-<your-validator-name>.json` file.
- [ ] Verified the chain-id and other parameters in my `gentx` file.
- [ ] Tested my `gentx` file with the latest network configuration.
```

# Repository Structure After Making It Public

Ensure your repository has the following structure after making it public:

```
mainnet-rehearsal/
├── gentx/
│   ├── gentx-example1.json
│   ├── gentx-example2.json
│   └── ... (additional gentx files)
├── README.md
└── ... (other files and directories)
```

# Additional Information

By following these steps, validators will be able to easily submit their `gentx` files via pull requests, and you will have a streamlined process for managing these submissions.


For more information on the WasmVM upgrade, refer to the [WasmVM v1.5.2 release](https://github.com/CosmWasm/wasmvm/releases/tag/v1.5.2).

We appreciate your cooperation in ensuring a smooth mainnet launch process. Please refactor and verify all files as needed.

Make sure to replace `<nodeName>` and `<keyName>` with the actual names you intend to use.

For any questions, we are here in our social media groups.

Thank you,  
The Soarchain Team
