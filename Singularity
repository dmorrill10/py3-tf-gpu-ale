Bootstrap: docker
From: tensorflow/tensorflow:1.5.0-gpu-py3

%environment
  # use bash as default shell
  SHELL=/bin/bash
  export SHELL

%setup
  # runs on host - the path to the image is $SINGULARITY_ROOTFS

%files
  /workspace/Arcade-Learning-Environment Arcade-Learning-Environment

%post
  # post-setup script

  # load environment variables
  . /environment

  # use bash as default shell
  echo 'SHELL=/bin/bash' >> /environment
  chmod +x /environment

  # default mount paths
  mkdir -p /scratch /data /usr/bin

  apt-get update
  apt-get install -y cmake libcupti-dev libyaml-dev wget unzip
  apt-get clean

  pip3 install --upgrade pip
  pip3 install numpy tqdm

  wget https://github.com/mgbellemare/Arcade-Learning-Environment/archive/v0.6.0.zip
  unzip Arcade-Learning-Environment-0.6.0.zip
  cd Arcade-Learning-Environment-0.6.0
  rm -rf build
  mkdir build
  cd build
  cmake -DUSE_SDL=OFF -DUSE_RLGLUE=OFF -DBUILD_EXAMPLES=OFF ..
  make -j 4

  cd ../
  pip3 install .

%runscript
  # executes with the singularity run command
  # delete this section to use existing docker ENTRYPOINT command

%test
  # test that script is a success
