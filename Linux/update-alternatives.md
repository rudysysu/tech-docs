# Summary

[TOC]

update-alternatives - maintain symbolic links determining default commands

# Command

update-alternatives

- --install link name path priority [--slave link name path]...
	* Add  a  group of alternatives to the system. 
	* update-alternatives --install /usr/bin/java java /usr/local/java/bin/java 1072
- --display name
	* Display information about the link group.
	* update-alternatives --display java
- --config name
	* Show available alternatives
	* update-alternatives --config java
