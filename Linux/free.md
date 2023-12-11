buffer与cache的区别
A buffer is something that has yet to be “written” to disk. 
A cache is something that has been “read” from the disk and stored for later use 
从应用程序角度来看，buffers/cached 是等于可用的，因为buffer/cached是为了提高文件读写的性能，当应用程序需在用到内存的时候，buffer/cached会很快地被回收。
所以从应用程序的角度来说，可用内存 = 系统free memory + buffers + cached.
