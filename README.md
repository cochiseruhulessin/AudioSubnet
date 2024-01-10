# Audio Generation Subnetwork

This subnetwork is a decentralized system designed for text-to-audio applications within the Bittensor network. It consists of a Validator and a Miner working collaboratively to generate high-quality audio from provided prompts. 
In the first phase, we will start with text-to-speech (TTS), working in parallel to add music generation in the upcoming updates. 

## Validators

The Validators are responsible for initiating the generation process by providing prompts to the Miners on the network. These prompts serve as the input text for the subsequent TTS model. The Validators evaluate the quality of the generated audio produced by the Miners and reward them based on the perceived quality.


## Miners

Miners in the Audio Subnetwork are tasked with generating audio from the text prompts received from the Validators. Leveraging advanced text-to-speech models, miners aim to produce high-fidelity, natural-sounding voice recordings. The quality of the generated audio is crucial, as it directly influences the miners' rewards.

## Workflow

1. **Prompt Generation:** The Validators generates prompts and distributes them to the Miners on the network.

2. **Text-to-Speech Processing:** Miners receive the prompts and utilize text-to-speech models to convert the text into voice audio.

3. **Quality Evaluation:** The Validator assesses the quality of the generated audio, considering factors such as: clarity, naturalness, and adherence to the prompt.

4. **Reward Distribution:** Based on the quality assessment, the Validator rewards Miners accordingly. Miners with consistently higher-quality outputs receive a larger share of rewards.

## Benefits

- **Decentralized Text-to-Speech:** The subnetwork decentralizes the TTS process, distributing the workload among participating Miners.
  
- **Quality Incentives:** The incentive mechanism encourages Miners to continually improve the quality of their generated voice audio.

- **Bittensor Network Integration:** Leveraging the Bittensor network ensures secure and transparent interactions between Validators and Miners.

Join the Audio Subnetwork and contribute to the advancement of decentralized text-to-speech / text-to-music technologies within the Bittensor ecosystem.


## Installation
```bash 
git clone https://github.com/UncleTensor/AudioSubnet.git
cd AudioSubnet
git checkout main
pip install -r requirements.txt
python -m pip install -e . 
```

## Recommended GPU Configuration

For optimal performance, it is recommended to use NVIDIA GeForce RTX 3090 GPUs for both Validators and Miners.


**Evaluation Mechanism:**
The evaluation mechanism involves the validator querying miners on the network with random prompts and receiving text-to-speech responses. These responses are scored based on correctness, and the weights on the Bittensor network are updated accordingly. The scoring is conducted using a reward function from the lib module.

**Miner/Validator Hardware Specs:**
The hardware requirements for miners and validators vary depending on the complexity and resource demands of the selected text-to-speech models. Typically, a machine equipped with a capable CPU and GPU, along with sufficient VRAM and RAM, is necessary. The amount of disk space required will depend on the size of the models and any additional data.

**How to Run a Validator:**
To operate a validator, you need to run the validator.py script with the required command-line arguments. This script initiates the setup of Bittensor objects, establishes a connection to the network, queries miners, scores their responses, and updates weights accordingly.

**How to Run a Miner:**
To operate a miner, run the miner.py script with the necessary configuration. This process involves initializing Bittensor objects, establishing a connection to the network, and processing incoming text-to-speech requests.

**Text-to-Speech Models Supported:**
The code incorporates three text-to-speech models: Microsoft/speecht5_tts, Facebook/mms-tts-eng and SunoBark. However, the specific requirements for each model, including CPU, GPU VRAM, RAM, and disk space, are not explicitly stated in the provided code. To ascertain these requirements, it may be necessary to consult the documentation or delve into the implementation details of these models.

In general, the resource demands of text-to-speech models can vary significantly. Larger models often necessitate more powerful GPUs and additional system resources. It is advisable to consult the documentation or model repository for the specific requirements of each model. Additionally, if GPU acceleration is employed, having a compatible GPU with enough VRAM is typically advantageous for faster processing.

## Auto-Update Feature

The Auto-Update feature in the Audio Subnetwork ensures that the software components, including text-to-speech models and other dependencies, remain up-to-date with the latest improvements and bug fixes. This feature is designed to:

1. **Automatically Check for Updates:** Periodically scans for new updates or patches available in the repository.
2. **Seamless Integration:** Integrates updates without disrupting ongoing processes or requiring manual intervention.
3. **Enhanced Security and Performance:** By keeping the software up-to-date, it ensures enhanced security and optimal performance.
4. **User Notification:** Notifies users about the updates being installed, allowing them to be aware of the changes and improvements.

To enable this feature, ensure you `--auto_update` argument with the value `yes`

Below are instructions for using the arguments in `miner.py` and `validator.py`:

# Instructions for `miner.py`:

## Miner Command
```bash
python neurons/miner.py \
    --netuid 16 \
    --wallet.name {wallet_name} \
    --wallet.hotkey {hotkey_name} \
    --logging.debug \
    --auto_update yes \
    --clone_model elevenlabs/eleven \
    --model elevenlabs/eleven \
    --eleven_api {elevenlabs_api_key} \
    --axon.port {machine_port}

```

### Bittensor Miner Script Arguments:

| **Category**                   | **Argument**                         | **Default Value**          | **Description**                                                                                                       |
|---------------------------------|--------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------|
| **Text To Speech Model**    | `--model`                            | Default: 'elevenlabs/eleven' ; 'microsoft/speecht5_tts' ; 'facebook/mms-tts-eng' ; 'suno/bark'   | The model to use for text-to-speech.                                                                                 |
| **Network UID** | `--netuid`                           |  Mainnet: 16        | The chain subnet UID. |
| **Voice Clone Model** | `--clone_model`                           |  'elevenlabs/eleven'       | The model to use for VOice Clone |
| **ElevenLabs API token** | `--eleven_api`                           |  Mandatory       | The API key to use for ElevenLabs Model |
| **Bittensor Subtensor Arguments** | `--subtensor.chain_endpoint`        | -                          | Endpoint for Bittensor chain connection.                                                                              |
|                                 | `--subtensor.network`                | -                          | Bittensor network endpoint.                                                                                          |
| **Bittensor Logging Arguments** | `--logging.debug`                    | -                          | Enable debugging logs.                                                                                               |
| **Bittensor Wallet Arguments**  | `--wallet.name`                      | -                          | Name of the wallet.                                                                                                  |
|                                 | `--wallet.hotkey`                    | -                  | Hotkey path for the wallet.                                                                                          |
| **Bittensor Axon Arguments**    | `--axon.port`                        | -                          | Port number for the axon server.                                                                                    |
| **Auto Update Argument**       | `--auto_update`                        | yes                          | Updates the repository                                                                                     |


# Instructions for `validator.py`:

### Voice Clone Service
Run the validator with the following command, replacing `{wallet_name}`, `{hotkey_name}`, and `{huggingface_access_token}` with your wallet and hotkey names and HuggingFace access token. Place your audio files (e.g., `audio01.wav`) and text files with the corresponding name (e.g., `audio01.txt`) in the `vc_source` folder for custom voice cloning. Once the files are processed, they will be moved to `vc_processed` folder. The voice cloned output will be saved in the `vc_target` folder.

### Text-to-Speech (TTS) Service
- For prompts from HuggingFace, set your HuggingFace access token.
- For custom prompts, place a CSV file named `tts_prompts.csv` in the `tts_source` directory. Audio outputs will be stored in the `tts_target` directory.

## Validator Command  
```bash
python neurons/validator.py \
    --netuid 16 \
    --wallet.name {wallet_name} \
    --wallet.hotkey {hotkey_name} \
    --logging.debug \
    --auto_update yes \
    --hub_key {huggingface_access_token}
```

### Bittensor Validator Script Arguments:

| **Category**                   | **Argument**                         | **Default Value**          | **Description**                                                                                                       |
|---------------------------------|--------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------|
| **Configuration Arguments**     | `--alpha`                            | 0.9                        | The weight moving average scoring.                                                                                    |
|                                 | `--netuid`                           |  Mainnet: 16                          | The chain subnet UID.                                                                                                 |
| **HuggingFace Access Token** | `--hub_key`                          | Mandatory                       | Supply the Huggingface Hub API key for the prompt dataset.                                                            |
| **Bittensor Subtensor Arguments** | `--subtensor.chain_endpoint`        | -                          | Endpoint for Bittensor chain connection.                                                                              |
|                                 | `--subtensor.network`                | -                          | Bittensor network endpoint.                                                                                          |
| **Bittensor Logging Arguments** | `--logging.debug`                    | -                          | Enable debugging logs.                                                                                               |
| **Bittensor Wallet Arguments**  | `--wallet.name`                      | -                          | Name of the wallet.                                                                                                  |
|                                 | `--wallet.hotkey`                    | -                  | Hotkey path for the wallet.                                                                                          |
| **Auto Update Argument**       | `--auto_update`                        | yes                          | Updates the repository                                                                                     |


## License
This repository is licensed under the MIT License.

```text
MIT License

Copyright (c) 2024 Opentensor

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```