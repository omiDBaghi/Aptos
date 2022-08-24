
# Aptos AIT3 Registration

To participate in the AIT-3 program, follow the below steps. Use these steps as a checklist to keep track of your progress. Click on the links in each step for a detailed documentation.

### Hardware requirements:
#### For running an Aptos node on incentivized testnet we recommend the following:
- CPU: 8 cores (Intel Xeon Skylake or newer)
- Memory: 32GB RAM
- Storage: 300GB (You have the option to start with a smaller size and adjust based upon demands)

### Set up your aptos validator
#### Option 1 (automatic)
Use script below for a quick installation
```
wget -qO aptos_validator.sh https://raw.githubusercontent.com/omiDBaghi/aptos/main/aptos_validator.sh && chmod +x aptos_validator.sh && ./aptos_validator.sh
```

### Post installation
When installation is finished please load variables into system
```
source $HOME/.bash_profile
```

### Check your node health
1. Navigate to https://ait.aptos-node.info/
2. Enter your node public IP address and change `API port` to `80`
3. You should see data like in example below:

### Register your validator node
1. Come back to the Aptos Community page and register your node by clicking on Step 4: `NODE REGISTRATION` button.

2. Provide the details of your validator node on this node registration screen, all the public key information you need is in the `~/$WORKSPACE/keys/public-keys.yaml` file (please don't enter anything from private keys).
```
cat ~/$WORKSPACE/keys/public-keys.yaml
```

- *OWNER KEY*: the first wallet public key. From `Settings -> Credentials`
- *CONSENSUS KEY*: **consensus_public_key** from `public-keys.yaml`
- *CONSENSUS POP*: **consensus_proof_of_possession** from `public-keys.yaml`
- *ACCOUNT KEY*: **account_public_key** from `public-keys.yaml`
- *VALIDATOR NETWORK KEY*: **validator_network_public_key** from `public-keys.yaml`

4. Next, click on VALIDATE NODE. If your node passes healthcheck, you will be prompted to complete the identity verification process.
> The Aptos team will perform a node health check on your validator, using the Node Health Checker. When Aptos confirms that your node is healthy, you will be asked to complete the KYC process.

5. Wait for the selection announcement. If you are selected, the Aptos team will airdrop coins into your owner wallet address. If you do not see airdropped coins in your owner wallet, you were not selected.

## Useful commands
### Check validator node logs
```
docker logs -f testnet-validator-1 --tail 50
```

### Check sync status
```
curl 127.0.0.1:9101/metrics 2> /dev/null | grep aptos_state_sync_version | grep type
```

### Restart docker container
```
docker restart testnet-validator-1
```

## Clean up preveous installation
(**WARNING!**) Before this step make sure you have backed up your Aptos keys as this step will completely remove your Aptos working directory
```
cd ~/$WORKSPACE && docker-compose down; cd
rm ~/$WORKSPACE -rf
docker volume rm aptos-validator
unset NODENAME
```
