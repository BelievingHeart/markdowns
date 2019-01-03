[//]: # (#update-alternatives)
# [update-alternatives by example](https://askubuntu.com/questions/1028601/install-gcc-8-only-on-ubuntu-18-04)
```bash
1. Initialize an alternative
#/usr/bin/gcc is the symilink to make based on highest priority
#Here 800 is the highest priority, so the symilink points to /usr/bin/gcc-8
#--slave is used to specify the belonging properties of gcc so that when when gcc changes alternative they also changes
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 700 --slave /usr/bin/g++ g++ /usr/bin/g++-7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 800 --slave /usr/bin/g++ g++ /usr/bin/g++-8
#gcc is the alternative_group_name to refer when using --config, see below
```
1. Switch between alternatives
```txt
sudo update-alternatives --config gcc
There are 2 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path            Priority   Status
------------------------------------------------------------
* 0            /usr/bin/gcc-8   800       auto mode
  1            /usr/bin/gcc-7   700       manual mode
  2            /usr/bin/gcc-8   800       manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```
