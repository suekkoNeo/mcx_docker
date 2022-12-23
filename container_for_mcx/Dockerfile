FROM ubuntu:20.04
WORKDIR /app

RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apt update &&\
    apt upgrade &&\
    apt install -y \
    gcc-7 \
    g++-7 \
    git \
    curl \
    wget \
    make \ 
    gnupg \ 
    vim \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    llvm \
    libncursesw5-dev \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
    libopencv-dev \
    software-properties-common

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin &&\
    mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600 &&\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC &&\
    apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub &&\
    add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /" &&\
    apt-get update &&\
    apt-get -y install cuda-10-2

RUN distribution=$(. /etc/os-release;echo $ID$VERSION_ID) &&\
    curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg &&\
    curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    tee /etc/apt/sources.list.d/nvidia-container-toolkit.list &&\
    apt update &&\ 
    apt install -y nvidia-docker2

RUN git clone https://github.com/pyenv/pyenv.git $HOME/.pyenv &&\
    git clone https://github.com/pyenv/pyenv-virtualenv.git $HOME/.pyenv/plugins/pyenv-virtualenv &&\
    pyenv install 3.9.0 &&\
    pyenv virtualenv 3.9.0 predict_mcx