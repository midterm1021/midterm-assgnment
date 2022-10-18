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
Preparing to unpack .../890-vdpau-driver-all_1.4-3build2_amd64.deb ...
Unpacking vdpau-driver-all:amd64 (1.4-3build2) ...
Selecting previously unselected package proj-bin.
Preparing to unpack .../891-proj-bin_8.2.1-1_amd64.deb ...
Unpacking proj-bin (8.2.1-1) ...
Errors were encountered while processing:
 /tmp/apt-dpkg-install-jJpAHP/559-python3-catkin-pkg-modules_0.5.2-1_all.deb
 /tmp/apt-dpkg-install-jJpAHP/598-python3-rospkg-modules_1.4.0-1_all.deb
 /tmp/apt-dpkg-install-jJpAHP/599-python3-rosdistro-modules_0.9.0-1_all.deb
E: Sub-process /usr/bin/dpkg returned an error code (1)
ros2@ros2ubuntu:~$ sudo apt install ros-humble-ros-base
[sudo] password for ros2: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
ros-humble-ros-base is already the newest version (0.10.0-1jammy.20220909.041039)

# I do the sourcing in th bash file :

os2@ros2ubuntu:~$ source /opt/ros/humble/setup.bash
ros2@ros2ubuntu:~$

# After installing all of these packages I try to code with an example: with talker, and listener commands :

ros2@ros2ubuntu:~$ ros2 run demo_nodes_cpp talker
[INFO] [1665879914.985322644] [talker]: Publishing: 'Hello World: 1'
[INFO] [1665879915.985764722] [talker]: Publishing: 'Hello World: 2'
[INFO] [1665879916.985618902] [talker]: Publishing: 'Hello World: 3'
[INFO] [1665879917.985483234] [talker]: Publishing: 'Hello World: 4'
[INFO] [1665879918.985780864] [talker]: Publishing: 'Hello World: 5'

------------------------------------------------------------------------------

ros2@ros2ubuntu:~$ source /opt/ros/humble/setup.bash
ros2@ros2ubuntu:~$ ros2 run demo_nodes_py listener
[INFO] [1665880116.983412912] [listener]: I heard: [Hello World: 203]
[INFO] [1665880117.973022045] [listener]: I heard: [Hello World: 204]
[INFO] [1665880118.972562601] [listener]: I heard: [Hello World: 205]
[INFO] [1665880119.971714387] [listener]: I heard: [Hello World: 206]
[INFO] [1665880120.971544159] [listener]: I heard: [Hello World: 207]
[INFO] [1665880121.972925768] [listener]: I heard: [Hello World: 208]
[INFO] [1665880122.972702650] [listener]: I heard: [Hello World: 209]
[INFO] [1665880123.973300124] [listener]: I heard: [Hello World: 210]





Week_4 
Turtlesim Installtion

# First I try to install turtlesim packages and update them :

ros2@ros2ubuntu:~$ sudo apt update
Hit:1 http://packages.ros.org/ros2/ubuntu jammy InRelease                     
Hit:2 http://security.ubuntu.com/ubuntu jammy-security InRelease              
Hit:3 http://kr.archive.ubuntu.com/ubuntu jammy InRelease
Hit:4 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:5 http://kr.archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
3 packages can be upgraded. Run 'apt list --upgradable' to see them.
ros2@ros2ubuntu:~$ sudo apt install ros-humble-turtlesim
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
ros-humble-turtlesim is already the newest version (1.4.2-1jammy.20220908.233909).
ros2@ros2ubuntu:~$ sudo apt install ros-humble-turtlesim
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
ros-humble-turtlesim is already the newest version (1.4.2-1jammy.20220908.233909).
ros-humble-turtlesim set to manually installed.


# And I check whether the turtlesim packages is enabled or not :


ros2@ros2ubuntu:~$ ros2 pkg executables turtlesim
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
ros2@ros2ubuntu:~$ 


# After successfull done I try to run and see the turtle appears on the screen :


ros2@ros2ubuntu:~$ ros2 run turtlesim turtlesim_node
Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
[INFO] [1665882085.889021444] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1665882085.910151013] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]

![Screenshot from 2022-10-16 10-02-44](https://user-images.githubusercontent.com/115865095/196013102-54a79c87-ad05-42b5-882b-025ebdde521a.png)

ros2@ros2ubuntu:~$ ros2 run turtlesim turtle_teleop_key
Reading from keyboard
---------------------------
Use arrow keys to move the turtle.
Use G|B|V|C|D|E|R|T keys to rotate to absolute orientations. 'F' to cancel a rotation.
'Q' to quit.


[Screencast from 10-16-2022 10:07:15 AM.webm](https://user-images.githubusercontent.com/115865095/196013170-d9d46737-28ed-4296-b1a0-06b655e7a51f.webm)

![Screenshot from 2022-10-16 10-07-53](https://user-images.githubusercontent.com/115865095/196013172-a807c81c-a198-46f2-b41d-6ab38be1c1ae.png)


# I do some update and try to run RQT using rqt command :


ros2@ros2ubuntu:~$ sudo apt update
[sudo] password for ubuntu: 
Hit:1 http://packages.ros.org/ros2/ubuntu jammy InRelease
Hit:2 http://security.ubuntu.com/ubuntu jammy-security InRelease
Hit:3 http://kr.archive.ubuntu.com/ubuntu jammy InRelease
Hit:4 http://kr.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:5 http://kr.archive.ubuntu.com/ubuntu jammy-backports InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
56 packages can be upgraded. Run 'apt list --upgradable' to see them.
ros2@ros2ubuntu:~$
ros2@ros2ubuntu:~$ sudo apt install ~nros-humble-rqt*
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
ros-humble-rqt-bag is already the newest version (1.1.3-2jammy.20220909.040110).
ros2@ros2ubuntu:~$ rqt

![Screenshot from 2022-10-16 10-34-33](https://user-images.githubusercontent.com/115865095/196013742-7d50b134-cdd2-465e-ac28-5657fb5d652e.png)



# As you can see I did some expression I mean I added new coordinates for the turtle to spawn at, x float 1.0, and y float 1.0 like that :



![Screenshot from 2022-10-16 10-37-03](https://user-images.githubusercontent.com/115865095/196013849-e587f3a5-9e72-440f-87fc-36174aa506a2.png)



Week_5

Creating a simple publisher and subscriber (python)

Step_1 : Create a package

ros2 pkg create --build-type ament_python py_pubsub

![Screenshot from 2022-10-18 02-51-14](https://user-images.githubusercontent.com/115865095/196247971-fcfca134-0ab5-4fcf-aa30-bd69f1eed0a3.png)


Step_2 : Writing the publisher node

Navigate into ros2_ws/src/py_pubsub/py_pubsub
![Screenshot from 2022-10-18 02-59-04](https://user-images.githubusercontent.com/115865095/196249186-dadbca20-3b9c-4ab9-9dd6-df610d734cad.png)


Download the code using this command :

wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_publisher/examples_rclpy_minimal_publisher/publisher_member_function.py



Now there will be a new file named publisher_member_function.py adjacent to __init__.py. In order to see them we type ls and we can see publisher_member_function.py and __init__.py files on terminal. In order to open the files just type open before the name of the files : 


![Screenshot from 2022-10-18 03-14-10](https://user-images.githubusercontent.com/115865095/196251864-8d24c866-5a57-4151-903e-0366c5b0c09a.png)



![Screenshot from 2022-10-18 03-12-11](https://user-images.githubusercontent.com/115865095/196251501-5090ab06-b98e-4b8e-ac17-e436dc66cee1.png)


Step_3 : Adding dependencies :

Navigate to ros2_ws/src/py_pubsub and there is package.xml file. Open the file using open package.xml command : 

Afterr that set the file by filling with my email and licence in my repository

![Screenshot from 2022-10-18 03-50-21-1](https://user-images.githubusercontent.com/115865095/196271874-7bc9f86d-3317-4ad3-aeb7-e94f2bc57c3b.png)

And we add the dependencies after that :

![Screenshot from 2022-10-18 03-50-07](https://user-images.githubusercontent.com/115865095/196271482-a96743c3-d76f-4492-a1b5-a2a3c58ad8f1.png)


Add an entry point 


We open the setup.py file and match the maintainer, maintainer_email, description and license fields to your package.xml:

![Screenshot from 2022-10-18 03-50-21-1](https://user-images.githubusercontent.com/115865095/196273903-3493d639-09bf-4432-a87b-535ff5efa451.png)



After that the contents of the setup.cfg file should be correctly populated automatically, like so:

![Screenshot from 2022-10-18 03-51-46](https://user-images.githubusercontent.com/115865095/196274536-6014f5b8-e35c-46d4-9016-4a3ef3a359ab.png)


Steep_4 
Write the subscriber node


we navigate to ros2_ws/src/py_pubsub/pysub, and enter the following command :

wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py

![Screenshot from 2022-10-18 03-52-10-1](https://user-images.githubusercontent.com/115865095/196275429-b5fa2709-eb06-4081-9a9e-8b6afaba7ac0.png)


we open __init__.py, publisher_member_function.py, subscriber_member_function.py and fill the dependencies :

![Screenshot from 2022-10-18 03-52-39-1](https://user-images.githubusercontent.com/115865095/196276672-fc337768-6e9a-4afc-95d3-2b8fd75ef168.png)


Step_5 
Build and Run

![image](https://user-images.githubusercontent.com/115865095/196524527-e4115574-cac4-4221-943e-7c92f6a0eee4.png)

