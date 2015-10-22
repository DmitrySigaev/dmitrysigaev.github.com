
ls /etc/apt/sources.list.d/
sudo rm /etc/apt/sources.list.d/nodesource.list*
sudo apt-add-repository -r nodesourc

sudo apt purge nodejs
sudo apt update
sudo apt install nodejs-legacy
npm install ffi --save
sudo apt install npm
