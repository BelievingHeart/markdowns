[//]: # (#valgrind #helgrind #memcheck #drd)
## memcheck
*A general memery error detector*
1. Usage:
```txt
valgrind --log-file=memcheck.log --read-var-info=yes --leak-check=full <your_cxx_runtime>
```
- --read-var-info=yes *Give more details on where the error occurred.*

## helgrind
*The purpose of Helgrind is to detect issues with synchronization implementations within a multithreaded application.*
1. Usage:
```txt
valgrind --tool=helgrind --read-var-info=yes --log-file=helgrind.log <your_cxx_runtime>
```

## DRD
*DRD is very similar to Helgrind, in that it also detects issues with threading and synchronization in the application.*
1. The main ways in which DRD differs from Helgrind are the following:
- DRD uses less memory
- DRD doesn't detect locking order violations
- DRD supports detached threads
2. Usage:
```txt
valgrind --tool=drd --log-file=drd.log --read-var-info=yes <your_cxx_runtime>
```
3. NOTE that there might be a lot of false positives when using std::thread