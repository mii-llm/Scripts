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

per installare git
e git clone https://github.com/axolotl-ai-cloud/axolotl.git
cd axolotl
pip3 install packaging ninja
pip3 install wheel
pip3 install torch (controllate la vostra versione di cuda con nvidia-smi e seguite le istruzioni https://pytorch.org/)
pip3 install --no-build-isolation -e '.[flash-attn,deepspeed]'




