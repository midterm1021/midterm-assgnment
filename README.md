# midterm-assgnment

Week_3

Ros2 humble version installation (ubuntu_22.04)

#First of all I make sure that I have a locale which supports UTF-8

1_STEP

ros2@ros2ubuntu:~$ locale
LANG=en_US.UTF-8
LANGUAGE=en_US:
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC=ko_KR.UTF-8
LC_TIME=ko_KR.UTF-8
LC_COLLATE="en_US.UTF-8"
LC_MONETARY=ko_KR.UTF-8
LC_MESSAGES="en_US.UTF-8"
LC_PAPER=ko_KR.UTF-8
LC_NAME=ko_KR.UTF-8
LC_ADDRESS=ko_KR.UTF-8
LC_TELEPHONE=ko_KR.UTF-8
LC_MEASUREMENT=ko_KR.UTF-8
LC_IDENTIFICATION=ko_KR.UTF-8
LC_ALL=
ros2@ros2ubuntu:~$ sudo apt update && sudo apt install locales
[sudo] password for ros2: 
Sorry, try again.
[sudo] password for ros2: 
Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]     
Hit:2 http://kr.archive.ubuntu.com/ubuntu jammy InRelease                     
Get:3 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease [114 kB]
Fetched 1,672 kB in 9s (178 kB/s)                                             
Reading package lists... Done
  systemd-hwe-hwdb
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 143 not upgraded.
ros2@ros2ubuntu:~$ sudo locale-gen en_US en_US.UTF-8
Generating locales (this might take a while)...
  en_US.ISO-8859-1... done
  en_US.UTF-8... done
Generation complete.
ros2@ros2ubuntu:~$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ros2@ros2ubuntu:~$ export LANG=en_US.UTF-8
ros2@ros2ubuntu:~$ locale
LANG=en_US.UTF-8
LANGUAGE=en_US:
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC=ko_KR.UTF-8
LC_TIME=ko_KR.UTF-8
LC_COLLATE="en_US.UTF-8"
LC_MONETARY=ko_KR.UTF-8
LC_MESSAGES="en_US.UTF-8"
LC_PAPER=ko_KR.UTF-8
LC_NAME=ko_KR.UTF-8
LC_ADDRESS=ko_KR.UTF-8
LC_TELEPHONE=ko_KR.UTF-8
LC_MEASUREMENT=ko_KR.UTF-8
LC_IDENTIFICATION=ko_KR.UTF-8
LC_ALL=

2_STEP

# I add the ROS2 repository to the system. Before that I check whether the Ubuntu Universe repository is enabled or not.

ros2@ros2ubuntu:~$ apt-cache policy | grep universe
500 http://kr.archive.ubuntu.com/ubuntu jammy/universe amd64 Packages
     release v=22.04,o=Ubuntu,a=jammy,n=jammy,l=Ubuntu,c=universe,b=amd64
ros2@ros2ubuntu:~$ sudo apt install software-properties-common
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  systemd-hwe-hwdb
Use 'sudo apt autoremove' to remove it.
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for libglib2.0-0:amd64 (2.72.1-1) ...
Processing triggers for man-db (2.10.2-1) ...
ros2@ros2ubuntu:~$ sudo add-apt-repository universe
Adding component(s) 'universe' to all repositories.
Press [ENTER] to continue or Ctrl-c to cancel.
Hit:1 http://security.ubuntu.com/ubuntu jammy-security InRelease              
Hit:2 http://kr.archive.ubuntu.com/ubuntu jammy InRelease                     
Hit:3 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:4 http://kr.archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done

#I add ROS2 apt repository to the system. Before I authorze the GPG key wth that apt command :

ros2@ros2ubuntu:~$ sudo apt update && sudo apt install curl gnupg lsb-release
Hit:1 http://security.ubuntu.com/ubuntu jammy-security InRelease
Hit:2 http://kr.archive.ubuntu.com/ubuntu jammy InRelease
Hit:3 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:4 http://kr.archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
140 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Unpacking curl (7.81.0-1ubuntu1.4) ...
Setting up libcurl4:amd64 (7.81.0-1ubuntu1.4) ...
Setting up curl (7.81.0-1ubuntu1.4) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
ros2@ros2ubuntu:~$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

# I add the repository to the source list :

os2@ros2ubuntu:~$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# I update caches just after setting up the repository. I use the apt command again : 

ros2@ros2ubuntu:~$ sudo apt update
Hit:1 http://kr.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease            
Hit:3 http://kr.archive.ubuntu.com/ubuntu jammy-backports InRelease           
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease              
Get:5 http://packages.ros.org/ros2/ubuntu jammy InRelease [4,673 B]
Get:6 http://packages.ros.org/ros2/ubuntu jammy/main amd64 Packages [737 kB]
Fetched 742 kB in 6s (131 kB/s)   
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
142 packages can be upgraded. Run 'apt list --upgradable' to see them.
ros2@ros2ubuntu:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  python3-catkin-pkg python3-rosdistro python3-rospkg
The following packages will be upgraded:

os2@ros2ubuntu:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
Setting up gnome-shell (42.4-0ubuntu0.22.04.1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.1) ...

# I instal the full dektop then :

ros2@ros2ubuntu:~$ sudo apt install ros-humble-desktop
[sudo] password for ros2: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done

