
reference : https://wiki.seismic-unix.org/sudoc:su_installation

# pull an image 
sudo docker pull ubuntu:18.04

# create a container
xhost +
sudo docker run -it --name seismic_unix -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:ro ubuntu:18.04

# install the essential SU depenency
sudo apt-get update
apt-get install build-essential libx11-dev libxt-dev freeglut3 freeglut3-dev libxmu-dev libxi-dev gfortran

# download SU
mkdir /usr/local/su
cd /usr/local/su

# please download the SU package in  https://nextcloud.seismic-unix.org/index.php/s/LZpzc8jMzbWG9BZ

mkdir /usr/local/su/src
cd src/

vim ~/.bashrc
'''
export CWPROOT=/usr/local/su
export PATH=$PATH:$CWPROOT/bin:.
'''
source ~/.bashrc

cd configs/
cp Makefile.config_Linux_Ubuntu  $CWPROOT/src/Makefile.config
cd $CWPROOT/src/

make install
make xtinstall
make xminstall
make mglinstall 
make finstall
make sfinstall
suplane | suximage
