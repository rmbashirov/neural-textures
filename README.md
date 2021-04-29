
# NeuralTextures

This is repository with inference code for paper [**"StylePeople: A Generative Model of Fullbody Human Avatars"**](https://arxiv.org/pdf/2104.08363.pdf) (CVPR21).
This code is for the part of the paper describing video-based avatars. For inference of generative neural textures model refer to [this repository](https://github.com/saic-vul/style-people).

## Getting started
### Data
To use this repository you first need to download model checkpoints and some auxiliary files.

* Download the archive with data from [Google Drive](https://drive.google.com/drive/folders/1YcY3WtCGyq6c0cZIcCG1rll7HGZb_JXc?usp=sharing) and unpack it into `NeuralTextures/data/`. It contains:
	* checkpoints for generative model and encoder network (`data/checkpoint`)
	* SMPL-X parameters for samples from *AzurePeople* dataset to run inference script on (`data/smplx_dicts`)
	* Some auxiliary data (`data/uv_render` and `data/*.npy`)
* Download SMPL-X models (`SMPLX_{MALE,FEMALE,NEUTRAL}.pkl`) from [SMPL-X project page](https://smpl-x.is.tue.mpg.de/) and move them to `data/smplx/`

### Docker
The easiest way to build an environment for this repository is to use docker.

1. - Install `docker` and `nvidia-docker`, [set](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/user-guide.html#daemon-configuration-file) `nvidia` your default runtime for docker, [add](https://docs.docker.com/engine/install/linux-postinstall/) current user to docker group
2. Build docker images: `make build`
3. Run docker container: `make run`
It mounts root directory of the host system to `/mounted/` inside docker and sets cloned repository path as a starting directory.

## Usage   
For now the only scenario in this repository involves rendering an image of a person from *AzurePeople* dataset with giver SMPL-X parameters.

Example:
```
python render_azure_person.py --person_id=04 --smplx_dict_path=data/smplx_dicts/04.pkl --out_path=data/results/
```
will render a person with `id='04'` with SMPL-X parameters from `data/smplx_dicts/04.pkl` and save resulting images to `data/results/04`.

For ids of all 56 people consult [this table](assets/dataset_lookup.png)
