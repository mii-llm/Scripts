apri vscode ssh e aggiungi la config

Host LA_BESTIA
    HostName 213.171.185.111
    User ecuser

mkdir samu e ti crei una cartella cd
cd samu
poi ti crei un ambiente virtuale con 
sudo apt install python3.10-venv
python3 -m venv training_venv
source training_venv/bin/activate lo attivi

poi facciamo
sudo apt-get update
sudo apt-get install git

e sudo apt-get install python3-dev (ci servirà dopo)

installiamo cuda toolkit (che ci servirà per flash attention)
If nvidia-smi is working, that means you already have NVIDIA drivers installed correctly. However, having drivers working doesn't necessarily mean you have the CUDA toolkit installed (which is what nvcc needs).

You can check your current CUDA version with:

bash

nvcc --version
Since you showed it's CUDA 11.5 and flash-attention requires CUDA 11.7 or higher, you do need to upgrade your CUDA toolkit. However, you don't need to remove your drivers.

You can install a newer CUDA toolkit alongside your existing one. Here's a shorter version:

bash

wget https://developer.download.nvidia.com/compute/cuda/12.3.1/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.1-545.23.08-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.1-545.23.08-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
Then set your CUDA_HOME:

bash

export CUDA_HOME=/usr/local/cuda
After that, try installing flash-attention again:

bash

pip install flash-attn --no-build-isolation




per installare git
e git clone https://github.com/axolotl-ai-cloud/axolotl.git
modificare evaluate==0.4.3 nei requirements di axolotl per far andare bench eval

cd axolotl
pip3 install packaging ninja
pip3 install wheel
pip3 install torch (controllate la vostra versione di cuda con nvidia-smi e seguite le istruzioni https://pytorch.org/)
pip3 install --no-build-isolation -e '.[flash-attn,deepspeed]'

ora creiamo una cartella in example chiamata minerva e ci mettiamo la config fornita dalla guida e poi lanciamo da axololt


 CUDA_VISIBLE_DEVICES="" axolotl preprocess examples/minerva/minerva.yml 

poi mi loggherei su hf se dataset o modello sono privati con huggingface-cli login e poi ottimizziamo il training su una gpu facendo delle prove con

 CUDA_VISIBLE_DEVICES="0" axolotl train examples/minerva/minerva.yml  

 lavoriamo solo con 1 gpu












