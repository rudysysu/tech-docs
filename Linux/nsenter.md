$ wget https://www.kernel.org/pub/linux/utils/util-linux/v2.24/util-linux-2.24.tar.gz; tar xzvf util-linux-2.24.tar.gz  
$ cd util-linux-2.24  
$ ./configure --without-ncurses && make nsenter  
$ sudo cp nsenter /usr/local/bin
