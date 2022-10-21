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

![Screenshot from 2022-10-21 03-32-43](https://user-images.githubusercontent.com/115865095/197029820-999896c0-5d54-494b-af0a-cad835d4b599.png)


ros2@ros2ubuntu:~$ source /opt/ros/humble/setup.bash
ros2@ros2ubuntu:~$ ros2 run demo_nodes_py listener

![image](https://user-images.githubusercontent.com/115865095/197030218-2f60bd75-2380-4324-9797-7bccecc38244.png)



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


Step_4 
Write the subscriber node


we navigate to ros2_ws/src/py_pubsub/pysub, and enter the following command :

wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py

![Screenshot from 2022-10-18 03-52-10-1](https://user-images.githubusercontent.com/115865095/196275429-b5fa2709-eb06-4081-9a9e-8b6afaba7ac0.png)


we open __init__.py, publisher_member_function.py, subscriber_member_function.py and fill the dependencies :

![Screenshot from 2022-10-18 03-52-39-1](https://user-images.githubusercontent.com/115865095/196276672-fc337768-6e9a-4afc-95d3-2b8fd75ef168.png)


Step_5 
Build and Run


To run rosdep in the root of your workspace (ros2_ws) to check for missing dependencies before building :

(from now on I am using another wmware terminal just because of some problems in my 'ro2@ros2ubuntu' named terminal. Please do not be in doubt with another named terminal, this is also mine.)
![image](https://user-images.githubusercontent.com/115865095/196524527-e4115574-cac4-4221-943e-7c92f6a0eee4.png)
 Then we build a new package in the root of ros2_ws
 
colcon build --packages-select py_pubsub

After that open a new terminal and source the setup files

. install/setup.bash

![image](https://user-images.githubusercontent.com/115865095/196533129-7c5c6199-5df4-4b56-9a5a-12e8f60d7591.png)

We run the talker node with the command :

ros2 run py_pubsub talker

![image](https://user-images.githubusercontent.com/115865095/197040841-3a6ed1cf-f518-46ce-a746-447e1d00b852.png)
![Screenshot from 2022-10-21 04-37-19](https://user-images.githubusercontent.com/115865095/197042226-79635d99-dd5a-4963-b1bf-ec7bc1e285bb.png)





Open another terminal, source the setup files from inside ros2_ws again, and then start the listener node:

ros2 run py_pubsub listener
The listener will start printing messages to the console, starting at whatever message count the publisher is on at that time, like so:


![image](https://user-images.githubusercontent.com/115865095/197041113-f34b241c-7362-4d12-a147-9f1c8ad5627d.png)
![image](https://user-images.githubusercontent.com/115865095/197040165-7f959096-137c-45d8-aefe-fe7766b01aa5.png)




Week_6
Write a Simple Service and Client

Step 1

#Recall that packages should be created in the src directory, not the root of the workspace. Navigate into ros2_ws/src and create a new package:

![Screenshot from 2022-10-19 19-17-02](https://user-images.githubusercontent.com/115865095/196664428-4dc4dc95-e8d6-449c-921b-213d33896c84.png)

Step 2

# make sure to add the description, maintainer email and name, and license information to package.xm : 

![Screenshot from 2022-10-19 19-21-42](https://user-images.githubusercontent.com/115865095/196665277-1294a4fc-c86b-45f3-9051-fece9a3d5d39.png)


![image](https://user-images.githubusercontent.com/115865095/196666339-8b61ae6d-e64b-4413-83b8-c192b998443d.png)


Step 3

#Adding an entry point :

![image](https://user-images.githubusercontent.com/115865095/196667692-f28e1e52-5490-43b7-8460-e1c403a3d9fc.png)


Step 4

Write the client node

 create a new file called client_member_function.py and paste the following code :
 
 ![image](https://user-images.githubusercontent.com/115865095/196668593-b6402a4b-2861-44e1-9a13-94a89f1d1f0c.png)


Step 5

Add an entry point
The entry_points field of your setup.py file should look like this :

![image](https://user-images.githubusercontent.com/115865095/196669339-446744b3-bda5-46d4-93f9-df1db4324894.png)

Step 6

Build and Run

in the root of your workspace (ros2_ws) to check for missing dependencies before building :

rosdep install -i --from-path src --rosdistro humble -y

# Navigate back to the root of your workspace, ros2_ws, and build your new package : 

colcon build --packages-select py_srvcli

Open a new terminal, navigate to ros2_ws, and source the setup files :

. install/setup.bash

Now run the service node:

ros2 run py_srvcli service

Open another terminal and source the setup files from inside ros2_ws again. Start the client node, followed by any two integers separated by a space :

ros2 run py_srvcli client 2 3


Part_2


Creating custom msg and srv files

Step 1

# Create a new package

Navigate to ros2_ws/src and install a package named "tutorial interfaces" :

ros2 pkg create --build-type ament_cmake tutorial_interfaces

![image](https://user-images.githubusercontent.com/115865095/197050155-60010df5-6c06-4107-9480-018e22f8819b.png)

# Then create two new folders :

![image](https://user-images.githubusercontent.com/115865095/197050653-ae9cde64-5e58-4c27-b6bb-e8fcc9856668.png)

Step msg definition


# In the tutorial_interfaces/msg directory you just created, make a new file called Num.msg with one line of code declaring its data structure:

int64 num

![image](https://user-images.githubusercontent.com/115865095/197051166-9ce1fdbd-e3de-4cb5-a617-5946536df1e4.png)


# And next to the Num.msg, create a file called Sphere.msg

![image](https://user-images.githubusercontent.com/115865095/197051657-c2a9dbf3-1bf8-4b33-ab22-2318bfd65cc8.png)


Step 3 srv definition

# Back to tutorial_interfaces/srv directory and make a new file called AddThreeInts.srv with the following request and response structure :

![image](https://user-images.githubusercontent.com/115865095/197101266-b93d6243-700c-48bf-828c-978d9bda5e56.png)


int64 a
int64 b
int64 c
---
int64 sum

![image](https://user-images.githubusercontent.com/115865095/197101401-e8dcbae7-35d0-4361-8232-2c37bd24cb7a.png)


Step 4

CMakeLists.txt

# To convert the interfaces you defined into language-specific code (like C++ and Python) so that they can be used in those languages, add the following lines to CMakeLists.txt :


find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Sphere.msg"
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)


Step 5

package.xml

# Add the following lines to package.xml


<depend>geometry_msgs</depend>

<build_depend>rosidl_default_generators</build_depend>

<exec_depend>rosidl_default_runtime</exec_depend>

<member_of_group>rosidl_interface_packages</member_of_group>


Step 6

Build the tutorial_interfaces package

# All the parts of custom interfaces package are in place, you can build the package. In the root of workspace (~/ros2_ws), run the following command:

colcon build --packages-select tutorial_interfaces


Step 7

Confirm msg and srv creation

# n a new terminal, run the following command from within your workspace (ros2_ws) to source it :

. install/setup.bash

# It is time to confirm that interface creation worked by using the ros2 interface show command :

ros2 interface show tutorial_interfaces/msg/Num

# It returns : 

int64 num

# And

ros2 interface show tutorial_interfaces/msg/Sphere

geometry_msgs/Point center
        float64 x
        float64 y
        float64 z
float64 radius

# And

ros2 interface show tutorial_interfaces/srv/AddThreeInts

# And

int64 a
int64 b
int64 c
---
int64 sum

Step 8

Testing Num.msg with pub/sub

# Publisher :


#include <chrono>
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/msg/num.hpp"                                            // CHANGE

using namespace std::chrono_literals;

class MinimalPublisher : public rclcpp::Node
{
public:
  MinimalPublisher()
  : Node("minimal_publisher"), count_(0)
  {
    publisher_ = this->create_publisher<tutorial_interfaces::msg::Num>("topic", 10);  // CHANGE
    timer_ = this->create_wall_timer(
      500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }

private:
  void timer_callback()
  {
    auto message = tutorial_interfaces::msg::Num();                                   // CHANGE
    message.num = this->count_++;                                                     // CHANGE
    RCLCPP_INFO_STREAM(this->get_logger(), "Publishing: '" << message.num << "'");    // CHANGE
    publisher_->publish(message);
  }
  rclcpp::TimerBase::SharedPtr timer_;
  rclcpp::Publisher<tutorial_interfaces::msg::Num>::SharedPtr publisher_;             // CHANGE
  size_t count_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}

  
# Subscriber :


#include <functional>
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/msg/num.hpp"                                       // CHANGE

using std::placeholders::_1;

class MinimalSubscriber : public rclcpp::Node
{
public:
  MinimalSubscriber()
  : Node("minimal_subscriber")
  {
    subscription_ = this->create_subscription<tutorial_interfaces::msg::Num>(    // CHANGE
      "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
  }

private:
  void topic_callback(const tutorial_interfaces::msg::Num & msg) const  // CHANGE
  {
    RCLCPP_INFO_STREAM(this->get_logger(), "I heard: '" << msg.num << "'");     // CHANGE
  }
  rclcpp::Subscription<tutorial_interfaces::msg::Num>::SharedPtr subscription_;  // CHANGE
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalSubscriber>());
  rclcpp::shutdown();
  return 0;
}

# CMakeLists.txt :

#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)                      # CHANGE

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp tutorial_interfaces)    # CHANGE

add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp tutorial_interfaces)  # CHANGE

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})

ament_package()

# package.xml:

# Add the following line :

<depend>tutorial_interfaces</depend>

After making the above edits and saving all the changes, build the package :

colcon build --packages-select cpp_pubsub

# And I open two new terminals, source ros2_ws in each, and run :

ros2 run cpp_pubsub talker

ros2 run cpp_pubsub listener

![Screenshot from 2022-10-21 14-43-59](https://user-images.githubusercontent.com/115865095/197121564-4800b693-d466-4eb7-ba01-f8fd2b8336ff.png)

[INFO] [minimal_publisher]: Publishing: '0'
[INFO] [minimal_publisher]: Publishing: '1'
[INFO] [minimal_publisher]: Publishing: '2'


Step 9

Testing AddThreeInts.srv with service/client

# Change  the original two integer request srv to a three request integer request srv :

# Service :

#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/srv/add_three_ints.hpp"                                        // CHANGE

#include <memory>

void add(const std::shared_ptr<tutorial_interfaces::srv::AddThreeInts::Request> request,     // CHANGE
          std::shared_ptr<tutorial_interfaces::srv::AddThreeInts::Response>       response)  // CHANGE
{
  response->sum = request->a + request->b + request->c;                                      // CHANGE
  RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "Incoming request\na: %ld" " b: %ld" " c: %ld",  // CHANGE
                request->a, request->b, request->c);                                         // CHANGE
  RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "sending back response: [%ld]", (long int)response->sum);
}

int main(int argc, char **argv)
{
  rclcpp::init(argc, argv);

  std::shared_ptr<rclcpp::Node> node = rclcpp::Node::make_shared("add_three_ints_server");   // CHANGE

  rclcpp::Service<tutorial_interfaces::srv::AddThreeInts>::SharedPtr service =               // CHANGE
    node->create_service<tutorial_interfaces::srv::AddThreeInts>("add_three_ints",  &add);   // CHANGE

  RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "Ready to add three ints.");                     // CHANGE

  rclcpp::spin(node);
  rclcpp::shutdown();
}

# Client :


#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/srv/add_three_ints.hpp"                                       // CHANGE

#include <chrono>
#include <cstdlib>
#include <memory>

using namespace std::chrono_literals;

int main(int argc, char **argv)
{
  rclcpp::init(argc, argv);

  if (argc != 4) { // CHANGE
      RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "usage: add_three_ints_client X Y Z");      // CHANGE
      return 1;
  }

  std::shared_ptr<rclcpp::Node> node = rclcpp::Node::make_shared("add_three_ints_client");  // CHANGE
  rclcpp::Client<tutorial_interfaces::srv::AddThreeInts>::SharedPtr client =                // CHANGE
    node->create_client<tutorial_interfaces::srv::AddThreeInts>("add_three_ints");          // CHANGE

  auto request = std::make_shared<tutorial_interfaces::srv::AddThreeInts::Request>();       // CHANGE
  request->a = atoll(argv[1]);
  request->b = atoll(argv[2]);
  request->c = atoll(argv[3]);                                                              // CHANGE

  while (!client->wait_for_service(1s)) {
    if (!rclcpp::ok()) {
      RCLCPP_ERROR(rclcpp::get_logger("rclcpp"), "Interrupted while waiting for the service. Exiting.");
      return 0;
    }
    RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "service not available, waiting again...");
  }

  auto result = client->async_send_request(request);
  // Wait for the result.
  if (rclcpp::spin_until_future_complete(node, result) ==
    rclcpp::FutureReturnCode::SUCCESS)
  {
    RCLCPP_INFO(rclcpp::get_logger("rclcpp"), "Sum: %ld", result.get()->sum);
  } else {
    RCLCPP_ERROR(rclcpp::get_logger("rclcpp"), "Failed to call service add_three_ints");    // CHANGE
  }

  rclcpp::shutdown();
  return 0;
}

# CMakeLists.txt:

# Add the following lines (C++ only):


#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)         # CHANGE

add_executable(server src/add_two_ints_server.cpp)
ament_target_dependencies(server
  rclcpp tutorial_interfaces)                      # CHANGE

add_executable(client src/add_two_ints_client.cpp)
ament_target_dependencies(client
  rclcpp tutorial_interfaces)                      # CHANGE

install(TARGETS
  server
  client
  DESTINATION lib/${PROJECT_NAME})

ament_package()

# package.xml:

# Add the following line:


<depend>tutorial_interfaces</depend>


# After editing and saving all changes, we build the package :


colcon build --packages-select cpp_srvcli


# Then we open two new terminals, source ros2_ws in each, and run:

ros2 run cpp_srvcli server

ros2 run cpp_srvcli client 2 3 1



Week_7

Writing an action server and client

Step 1

Writing an action server

# Open a new file in your home directory, let’s call it fibonacci_action_server.py, and add the following code :


![Screenshot from 2022-10-20 00-41-20](https://user-images.githubusercontent.com/115865095/196739333-06375700-74b7-46ef-9c04-8a48c0e5f672.png)

# And we try to run our action server :

python3 fibonacci_action_server.py

![Screenshot from 2022-10-20 00-39-16](https://user-images.githubusercontent.com/115865095/196739820-6dfc55a1-9cfb-4b3d-b6c7-f0cc617b4280.png)

In another terminal, we can use the command line interface to send a goal :

ros2 action send_goal fibonacci action_tutorials_interfaces/action/Fibonacci "{order: 5}"

![Screenshot from 2022-10-20 00-44-56](https://user-images.githubusercontent.com/115865095/196740298-f031fe0b-645f-4f24-87e4-dee7cb9701c3.png)

# Now let’s make our goal execution actually compute and return the requested Fibonacci sequence:

![Screenshot from 2022-10-20 13-57-20](https://user-images.githubusercontent.com/115865095/196860243-a4ae64f8-db53-4d3d-8131-df773240f52d.png)

Step 2

Publishing feedback

# We’ll replace the sequence variable, and use a feedback message to store the sequence instead

![Screenshot from 2022-10-20 14-03-28](https://user-images.githubusercontent.com/115865095/196860795-1004afff-9d64-4e5b-8893-b3197ca81089.png)

Step 3

Writing an action client

# We’ll also scope the action client to a single file. Open a new file, let’s call it fibonacci_action_client.py, and add the following boilerplate code :

![Screenshot from 2022-10-21 02-01-48](https://user-images.githubusercontent.com/115865095/197012747-27a7c6d4-1b73-4f0f-80c1-e9a98ccd982f.png)

Let’s test our action client by first running the action server built earlier : 

python3 fibonacci_action_server.py


![Screenshot from 2022-10-21 02-07-50](https://user-images.githubusercontent.com/115865095/197014047-e8098cef-b571-4fc0-ba6b-b864a0c493c7.png)

ANd in another terminal we run the action client : 

python3 fibonacci_action_client.py

The action client should start up, and then quickly finish. At this point, we have a functioning action client, but we don’t see any results or get any feedback : 

![image](https://user-images.githubusercontent.com/115865095/197014304-279254ec-2e92-44aa-a868-ce921ce21558.png)

Step 4

Getting a result 

# Here’s the complete code for this example :

import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()


With an action server running in a separate terminal, go ahead and try running our Fibonacci action client :

python3 fibonacci_action_client.py

![Screenshot from 2022-10-21 03-11-49](https://user-images.githubusercontent.com/115865095/197026083-765c4b66-458f-4578-816c-da92f22be975.png)

Step 5

Getting a feedback

# Our action client can send goals. Nice! But it would be great if we could get some feedback about the goals we send from the action server.

# Here’s the complete code for this example :

import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node

from action_tutorials_interfaces.action import Fibonacci


class FibonacciActionClient(Node):

    def __init__(self):
        super().__init__('fibonacci_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def send_goal(self, order):
        goal_msg = Fibonacci.Goal()
        goal_msg.order = order

        self._action_client.wait_for_server()

        self._send_goal_future = self._action_client.send_goal_async(goal_msg, feedback_callback=self.feedback_callback)

        self._send_goal_future.add_done_callback(self.goal_response_callback)

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def get_result_callback(self, future):
        result = future.result().result
        self.get_logger().info('Result: {0}'.format(result.sequence))
        rclpy.shutdown()

    def feedback_callback(self, feedback_msg):
        feedback = feedback_msg.feedback
        self.get_logger().info('Received feedback: {0}'.format(feedback.partial_sequence))


def main(args=None):
    rclpy.init(args=args)

    action_client = FibonacciActionClient()

    action_client.send_goal(10)

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
    
![image](https://user-images.githubusercontent.com/115865095/197027461-84e34ed7-ca0e-4bbc-9153-477fbdd9910c.png)

 
 # We’re all set. If we run our action client, you should see feedback being printed to the screen.

  
 Part_2
  
  Step 1
  
  Composing multiple nodes in a single process
  
  # Checking what components are available in the workspace I am using :
  
  
  ros2 component types
  
  
  ![image](https://user-images.githubusercontent.com/115865095/197123055-910340d3-4bf8-46ba-a9f3-657e258ef4e9.png)
![image](https://user-images.githubusercontent.com/115865095/197123108-ae4cdaae-07e3-43ab-a2cb-7af8197063d7.png)

 
  
  The terminal will return the list of all available components:

(... components of other packages here)
composition
  composition::Talker
  composition::Listener
  composition::NodeLikeListener
  composition::Server
  composition::Client
(... components of other packages here)

 Step 2
  
Run-time composition using ROS services with a publisher and subscriber
  
 ros2 run rclcpp_components component_container
  
 # After that we open the second terminal workspace and try to verify the container is running or not with ros2 command line :
  
ros2 component list
  
![image](https://user-images.githubusercontent.com/115865095/197124062-37c95e6f-6cfd-46d6-9b09-1cc0e5ce06ae.png)

/ComponentManager
  
  
# we try to load the talker component in the second terminal we opened just before :
 
  
ros2 component load /ComponentManager composition composition::Talker
  
# The command will return the unique ID of the loaded component as well as the node name :

 
Loaded component 1 into '/ComponentManager' container node as '/talker'
 
  
 # We run another command to load listener in the second terminal again :
  
  
 ![image](https://user-images.githubusercontent.com/115865095/197127754-df2a0a0c-556b-4d76-a678-ca87bb7a7bc3.png)

 ros2 component load /ComponentManager composition composition::Listener
  
  
 # Terminal returns :
  
  ![image](https://user-images.githubusercontent.com/115865095/197127542-c7ed20ce-3b8d-449e-9704-8d18c41dc334.png)

 Loaded component 2 into '/ComponentManager' container node as '/listener'
  
 # ros2 command is now available to check the state of the container :
  
  ros2 component list
  
 # Result :
  
  
  ![image](https://user-images.githubusercontent.com/115865095/197128174-9a56bd71-9d4c-4098-b8b4-ef5a72956ffd.png)
![image](https://user-images.githubusercontent.com/115865095/197128240-bfbf03a2-a749-46be-8cfd-1f2476c1ba63.png)
[Screencast from 10-21-2022 03:28:50 PM.webm](https://user-images.githubusercontent.com/115865095/197128280-4eafe2b0-44e9-4277-9727-6d463583436a.webm)
  
 /ComponentManager
   1  /talker
   2  /listener
  
  
  Step 3
  
  
 Run-time composition using ROS services with a server and client
  
 # The example with a server and a client is very similar.


# In the first terminal :
  

ros2 run rclcpp_components component_container

![image](https://user-images.githubusercontent.com/115865095/197128663-79f06048-1c07-427c-bb4e-a4c913f89b57.png)

  
# In the second terminal :
 

ros2 component load /ComponentManager composition composition::Server
ros2 component load /ComponentManager composition composition::Client
 
![image](https://user-images.githubusercontent.com/115865095/197128558-ae4c0cc2-9260-4792-aca9-5c55ee95e784.png)


Step 4
  
  
Compile-time composition using ROS services
  
  
# In the terminal :
  
  
ros2 run composition manual_composition
 
![image](https://user-images.githubusercontent.com/115865095/197128856-da34e74d-391f-4ad8-8639-d650859a2aaf.png)

  
Step 5
  
  
Run-time composition using dlopen


# The process will open each library and create one instance of each “rclcpp::Node” class in the library source code).
 
ros2 run composition dlopen_composition `ros2 pkg prefix composition`/lib/libtalker_component.so `ros2 pkg prefix composition`/lib/liblistener_component.so
  
![image](https://user-images.githubusercontent.com/115865095/197129060-d7aa59d4-5f13-485c-9255-5f5850c990f6.png)

  

Step 6
  
Composition using launch actions
  

# To automate this action, we can use the functionality in ros2 launch :
  
 
ros2 launch composition composition_demo.launch.py
  
![image](https://user-images.githubusercontent.com/115865095/197129340-ab128f3e-0af4-4d87-a5a7-927fe3a77ba6.png)


----------------------------------------------------------------------------------------------
Advanced Topics 
----------------------------------------------------------------------------------------------
  
  
1. Unloading components
  

# In the first terminal  start the component container :
  
  
ros2 run rclcpp_components component_container
 
  
![image](https://user-images.githubusercontent.com/115865095/197129911-fea66810-2188-481d-9f5a-806e2099f163.png)

  
# Verify that the container is running via ros2 command line tools:
 
ros2 component list
  

![image](https://user-images.githubusercontent.com/115865095/197130402-5274768a-2140-4d27-95f0-e433c7de6387.png)

  
# In the second shell terminal we try to load both talker and listener we have before :
  
 ros2 component load /ComponentManager composition composition::Talker
ros2 component load /ComponentManager composition composition::Listener
  
 ![image](https://user-images.githubusercontent.com/115865095/197130774-828905e6-af8c-4383-abd6-14b4af4a6442.png)

  # The first terminal :

  
![image](https://user-images.githubusercontent.com/115865095/197130699-b6730dac-d991-48ad-8aff-d45caf88610c.png)


# Use the unique ID to unload the node from the component container :
  
 ros2 component unload /ComponentManager 1 2
  
 ![image](https://user-images.githubusercontent.com/115865095/197131080-a60be943-76b2-4ae3-87e8-3cdeee814eb8.png)

  
2. Remapping container name and namespace

  
# The component manager name and namespace can be remapped via standard command line arguments :
  
 
 ros2 run rclcpp_components component_container --ros-args -r __node:=MyContainer -r __ns:=/ns
 
 ![image](https://user-images.githubusercontent.com/115865095/197131667-338fb176-352b-4e07-b0fc-026b0fe00781.png)

  
  # In the second shell, components can be loaded by using the updated container name:

  ![image](https://user-images.githubusercontent.com/115865095/197131820-ffb5ff0a-c22b-4a20-8746-c4af291f9aa9.png)

3. Remap component names and namespaces


 # In the first shell, start the component container:
  
  
  ros2 run rclcpp_components component_container
  
  ![image](https://user-images.githubusercontent.com/115865095/197132106-3f522ef6-86c5-4f11-9e29-4e5405215984.png)

  
  # Remap node name:
  

ros2 component load /ComponentManager composition composition::Talker --nde-name talker2
  
  
  ![image](https://user-images.githubusercontent.com/115865095/197132549-51fdd707-8e2d-4444-894b-e5b9923c6343.png)

 ![image](https://user-images.githubusercontent.com/115865095/197132465-b20e42b6-7f7e-4788-ac55-ad7a6f0a6610.png)

 
  # Remap namespace :
  
  
  ros2 component load /ComponentManager composition composition::Talker --node-namespace /ns
  
  
  ![image](https://user-images.githubusercontent.com/115865095/197133863-40cba7c9-b029-4886-a175-fabefb832b3a.png)

  ![image](https://user-images.githubusercontent.com/115865095/197133779-b14d3f80-0d88-445d-839f-48dc12f56104.png)

  
  # Remap both:
  

ros2 component load /ComponentManager composition composition::Talker --node-name talker3 --node-namespace /ns2

 ![image](https://user-images.githubusercontent.com/115865095/197134140-ec315ae9-8c27-41d9-87d8-7db28e207ecc.png)

  ![image](https://user-images.githubusercontent.com/115865095/197134055-1353e4a0-8c92-4604-80e0-f095931e80cc.png)

# Now use ros2 command line utility:

  
ros2 component list

  
# In the console you should see corresponding entries:

  
  ![image](https://user-images.githubusercontent.com/115865095/197134302-02196288-27b2-44d4-8672-e7bbc297afb4.png)

/ComponentManager
   1  /talker2
   2  /ns/talker
   3  /ns2/talker3

  
4 . Passing parameter values into components
  
ros2 component load /ComponentManager image_tools image_tools::Cam2Image -p burger_mode:=true
  
  
 ![image](https://user-images.githubusercontent.com/115865095/197135256-cc50221b-4990-4491-9135-70428509fae8.png)
![image](https://user-images.githubusercontent.com/115865095/197134542-bf1a4d9b-b114-4a3f-9f2b-5be22083696e.png)
![image](https://user-images.githubusercontent.com/115865095/197135386-6e11fe50-fbba-425a-9cde-b14eb3b291d5.png)

  
  
5. Passing additional arguments into components
  

ros2 component load /ComponentManager composition composition::Talker -e use_intra_process_comms:=true
  
  ![image](https://user-images.githubusercontent.com/115865095/197135072-b207e61b-ad83-4953-b60d-679611a66da0.png)
 ![image](https://user-images.githubusercontent.com/115865095/197134893-91920a08-0264-412c-b8f0-ea386c65496d.png)
  ![image](https://user-images.githubusercontent.com/115865095/197135145-449ac096-8b52-4473-b642-d0125e3f3eac.png)


And I will finish the work in here.
