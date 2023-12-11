ln -s /opt/aaa-1.1.1 /opt/aaa
unlink /opt/aaa

ln -sn /opt/node_exporter-0.16.0.linux-amd64 /opt/node_exporter
不使用n，重复执行上面的命令会导致在目标软链下，又生成多个软件
