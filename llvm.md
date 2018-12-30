[//]: # (#clang++ #llvm #clang-tidy)
## Install
1. llvm on ubuntu 18.04
```bash
echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-7 main" | sudo tee /etc/apt/sources.list.d/llvm.list
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
sudo apt-get install clang-7 clang-tools-7 clang-tidy-7 libclang-common-7-dev libclang-7-dev libclang1-7 clang-format-7 python-clang-7 
```
- [REF_1](https://apt.llvm.org/)
- [REF_2](https://askubuntu.com/questions/233064/why-am-i-getting-command-deb-not-found/860763#860763?newreg=12885fb1903e4c3585e0c43d1f171203)


## Clang-tidy
1. fix code
 - Clang-tidy can only fix one translation unit
 - If you want to fix a project, use **run-clang-tidy**[:link:](https://github.com/KratosMultiphysics/Kratos/wiki/How-to-use-Clang-Tidy-to-automatically-correct-code)
 - NOTE: **do not** specify *-header-filter=.\** when some headers are included more than once in your project