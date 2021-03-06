### Setup CUDA drivers and PyTorch on GCP

Launch a new instance configured with Ubuntu 20.04 LTS and a GPU, clone this repository, and run the following:
#### Install CUDA
```bash
sudo ./install_cuda.sh
sudo reboot
# verify
nvidia-smi
```
#### Install R
```bash
sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
sudo apt install r-base
R --version
```
##### Install qvalue package in R
open R
```bash
R
```
```R
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("qvalue")
```

#### Install Python 3
```bash
sudo apt update
sudo apt install -y python3-pip python3-dev python3-virtualenv
pip3 install --upgrade pip virtualenv setuptools
virtualenv venv
source venv/bin/activate
pip3 install -r requirements.txt
# verify
python3 -c "import torch; print(torch.__version__); print('CUDA available: {} ({})'.format(torch.cuda.is_available(), torch.cuda.get_device_name(torch.cuda.current_device())))"
```

#### Install rmate (optional)
```bash
sudo apt install -y ruby
mkdir ~/bin
curl -Lo ~/bin/rmate https://raw.githubusercontent.com/textmate/rmate/master/bin/rmate
chmod a+x ~/bin/rmate
echo 'export RMATE_PORT=${rmate_port}' >> ~/.bashrc
```
