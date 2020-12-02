# OpenRAVE on Ubuntu 18.04

This package is modified from original repos to compile OpenRAVE on Ubuntu 18.04 + Boost 1.65.1

1. Install dependencies

```sh
sudo apt-get update

sudo apt-get install -y --no-install-recommends build-essential cmake doxygen \
  g++ git octave python-dev python-setuptools wget mlocate
  
sudo apt-get install -y --no-install-recommends ipython python-h5py python-numpy \
    python-pip python-wheel python-scipy
    
sudo apt-get install -y --no-install-recommends qt5-default minizip    

sudo apt-get install -y --no-install-recommends ann-tools libann-dev            \
libassimp-dev libavcodec-dev libavformat-dev libeigen3-dev libfaac-dev          \
libflann-dev libfreetype6-dev liblapack-dev libglew-dev libgsm1-dev             \
libmpfi-dev  libmpfr-dev liboctave-dev libode-dev libogg-dev libpcre3-dev       \
libqhull-dev libswscale-dev libtinyxml-dev libvorbis-dev libx264-dev            \
libxml2-dev libxvidcore-dev libbz2-dev

sudo apt-get install -y --no-install-recommends libsoqt-dev-common libsoqt4-dev

sudo apt-get install -y --no-install-recommends libccd-dev                  \
  libcollada-dom2.4-dp-dev liblog4cxx-dev libminizip-dev octomap-tools
  
#Install boost
sudo apt-get install -y --no-install-recommends libboost-all-dev libboost-python-dev

#Run this command to make sure you have installed Boost 1.65.1 successfully
dpkg -s libboost-all-dev | grep 'Version'
  
```

2. Build package
```sh
#clone this package to your local folder
git clone https://github.com/RIVeR-Lab/openrave.git

#build package using cmake
cd openrave
mkdir build; cd build
cmake ..
make -j `nproc`
sudo make install
```

3. Verify installation
```sh
#run this command to check if the library has been installed successfully
ls /usr/local/lib | grep libopenrave

```


4. Troubleshoot:
```sh
/usr/local/include/fcl/math/constants.h:131:1: error: expected primary-expression before ‘typedef’
 typedef typename detail::ScalarTrait<S>::type Real;
```
This error is caused by a conflict of different versions of FCL library. It's highly likely you have two versions of FCL (fcl0.6 and fcl0.5) installed on your computer. The default fcl library for 18.04 is fcl-0.5, so you need to consider which one to use and modify accordingly in the CMakeLists.txt. 
The easy solution would be deleting the locally installed version (fcl-0.6) by deleting /usr/local/include/fcl* and /usr/local/lib/libfcl*
