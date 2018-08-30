Bootstrap: docker
FROM: continuumio/miniconda3:latest

%labels
    Maintainer Jeremy Magland
    Version 0.1.0

%setup
  mkdir ${SINGULARITY_ROOTFS}/working
  cp -r . ${SINGULARITY_ROOTFS}/working/src

%post
  echo "################################## Activating conda environment"
  . /opt/conda/etc/profile.d/conda.sh
  conda create -n env1
  conda activate env1

  echo "################################## Installing MountainLab"
  conda install -c flatiron -c conda-forge mountainlab

  echo "################################## Installing Python"
  conda install python=3.6

  echo "################################## Installing ML package"
  cd /working/src
  pip install .
  ml-link-python-module ml_ephys `ml-config package_directory`/ml_ephys

  echo "################################## Testing package"
  ml-list-processors

%environment
  . /opt/conda/etc/profile.d/conda.sh
  conda activate env1