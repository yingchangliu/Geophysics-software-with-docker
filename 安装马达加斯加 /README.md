Install Madagascar on ubuntu:18.04 docker image.

I use the openSUSE Tumbleweed and WSL (Windows Subsystem for Linux), but it is troublesome to configure dependencies, so I choose to use docker. Since it has been implemented to run the GUI on docker before, this is very practical.

It is very easy, just reproduce the official website ( http://www.ahay.org/ ) tutorial.

# pull an image 
sudo docker pull ubuntu:18.04

# create a container
sudo docker run -it --name madagascar -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:ro ubuntu:18.04

# install the essential Madagascar depenency
sudo apt-get update
sudo apt-get install libxaw7-dev freeglut3-dev libnetpbm10-dev libgd-dev libplplot-dev libavcodec-dev libcairo2-dev libjpeg-dev swig python-dev python-numpy g++ gfortran libopenmpi-dev libfftw3-dev libsuitesparse-dev python-epydoc scons git emacs25

# download madagascar
mkdir /home/Document/madagascar
cd /home/Document/madagascar
git clone https://github.com/ahay/src RSFSRC

# install it
cd RSFSRC
./configure --prefix=/usr/local/RSFROOT
./configure API=c++,f90 --prefix=/usr/local/RSFROOT
sudo make install

# configure the environment
sudo vim ~/.bashrc
'''
source /home/Document/madagascar/env.sh
'''
# or you can input : echo "source /home/Document/madagascar/env.sh" >> ~/.bashrc
cd ~
source .bashrc

# test it now!
sfmath n1=1000 output='sin(0.5*x1)' > sin.rsf
<sin.rsf sfwiggle | sfpen
