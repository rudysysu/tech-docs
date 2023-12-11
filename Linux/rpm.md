列出rpm包内容和解压rpm包内容

列出rpm包的内容：
rpm -qpl *.rpm

解压rpm包的内容：（没有安装，就像解压tgz包一样rpm包）
rpm2cpio *.rpm | cpio -div
