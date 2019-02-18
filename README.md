# Welle cli Web Interface
Welle cli Web Interface

## Installation de rtl-sdr

    $ sudo apt-get install cmake libusb-1.0-0.dev build-essential
    $ git clone git://git.osmocom.org/rtl-sdr.git
    $ cd rtl-sdr/
    $ mkdir build
    $ cd build
    $ cmake ../ -DINSTALL_UDEV_RULES=ON
L’option -DINSTALL_UDEV_RULES=ON   permet de lancer rtl-sdr sans être root

    $ sudo ldconfig
    $ sudo reboot

## Installation de Welle.io-Web-CLI

    $ sudo apt-get install automake librtlsdr-dev libmp3lame-dev libfaad-dev pkg-config libfftw3-dev libmpg123-dev
    $ sudo chmod 777 /usr/src/
    $ cd /usr/src
    $ git clone https://github.com/AlbrechtL/welle.io
    $ cd welle.io
    $ git checkout next
    $ mkdir build
    $ cd build
    $ CFLAGS="-ffast-math" CXXFLAGS="-ffast-math" cmake .. -DRTLSDR=ON -DBUILD_WELLE_IO=OFF
    $ make -j 4
    
## Installation et configuration de Supervisor

    $ sudo apt-get install supervisor
    $ mkdir config && cd config
    $ mkdir supervisor && cd supervisor
    $ wget https://raw.githubusercontent.com/LyonelB/Welle-cli-Web-Interface/master/welleio.conf
    $ cd
    $ sudo ln -s /home/pi/config/supervisor/welleio.conf /etc/supervisor/conf.d/welleio.conf
    $ sudo nano /etc/supervisor/supervisord.conf    

Ajoutez les lignes suivantes

[inet_http_server]  
port = 9400  
username = user ; Auth username  
password = pass ; Auth password  
    
    $ sudo /etc/init.d/supervisor restart
    
Il ne vous reste plus qu'à vous rendre à l'url : http://ip.de.votre.raspberry:7979
