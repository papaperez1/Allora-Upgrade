# Allora-Upgrade - Run A Model Predicting Prices using Hugging Face Model with topic 1 to 9

![image](https://github.com/user-attachments/assets/c4eda80a-41ed-4008-8463-9cd51e33eb7e)

## For New Users

follow till 'Wallet Setup' section from https://github.com/papaperez1/Allora/blob/main/README.md and come back to this guide.

## For Exisitng users

### Cleanup existing containers

If you already have a runnnig worker, first remove the docker containers and cleanup the worker directory

```
cd $HOME && cd basic-coin-prediction-node
docker compose down -v
docker container prune
```
```
cd ..
rm -rf basic-coin-prediction-node
```


### Clone HuggingFace worker

```
cd $HOME
git clone https://github.com/allora-network/allora-huggingface-walkthrough
cd allora-huggingface-walkthrough
```
```
mkdir -p worker-data
chmod -R 777 worker-data
```
```
rm config.example.json
nano config.json
```
COpy below code and paste inside the file. Make sure you Update SeedPhrase
```
{
    "wallet": {
        "addressKeyName": "testkey",
        "addressRestoreMnemonic": "SeedPhrase",
        "alloraHomeDir": "/root/.allorad",
        "gas": "1000000",
        "gasAdjustment": 1.0,
        "nodeRpc": "https://rpc.ankr.com/allora_testnet",
        "maxRetries": 1,
        "delay": 1,
        "submitTx": false
    },
    "worker": [
        {
            "topicId": 1,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 1,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "ETH"
            }
        },
        {
            "topicId": 2,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 3,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "ETH"
            }
        },
        {
            "topicId": 3,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 5,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "BTC"
            }
        },
        {
            "topicId": 4,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 2,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "BTC"
            }
        },
        {
            "topicId": 5,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 4,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "SOL"
            }
        },
        {
            "topicId": 6,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 5,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "SOL"
            }
        },
        {
            "topicId": 7,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 2,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "ETH"
            }
        },
        {
            "topicId": 8,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 3,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "BNB"
            }
        },
        {
            "topicId": 9,
            "inferenceEntrypointName": "api-worker-reputer",
            "loopSeconds": 5,
            "parameters": {
                "InferenceEndpoint": "http://inference:8000/inference/{Token}",
                "Token": "ARB"
            }
        }
        
    ]
}
```
CTRL+X+Y to save the changes

### Create coingecko API
https://www.coingecko.com/en/developers/dashboard

Replace Coingecko API in app.py

```
nano app.py
```
![image](https://github.com/user-attachments/assets/106786f7-9cd7-4e43-ab0d-363b29e87c34)

CTRL+X+Y+Enter to save & exit

### Run Huggingface Worker

```
chmod +x init.config
./init.config
```
```
docker compose up --build -d
```
```
docker compose logs -f worker | grep Success
```
GO back to your dashboard https://shorturl.at/1nlGM - connect wallet and check points





References: 0xmoei & https://docs.allora.network/home/explore
