# Vinebot_ROS_Packages 

The set of packages for the Vinebot robot 

HERE you can find all the nesseccary Vinebot ROS packages up to date!

# Install

Clone on your catkin workspace this repository, download all dependencies and compile!

```bash
# Make catkin workspace if does not exist and clone this repo
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
git clone https://github.com/yerkgb/Vinebot_ROS_Packages.git
# Install all dependecies
cd ..
rosdep install --from-paths src --ignore-src -r -y
# Compile package
catkin_make
```

This package is binding the USD devices under static name, so you can install the udev rule to identify the device as given in launch files. In order to do so edit /etc/udev/rules.d/10-local.rules file under root user:
```bash
$sudo su root 
$nano /etc/udev/rules.d/99-usb-serial.rules
#add the following line inside the file 
SUBSYSTEM=="tty", ATTRS{idVendor}=="067b", ATTRS{idProduct}=="23f3", SYMLINK+="roboteq"
SUBSYSTEM=="tty", ATTRS{idVendor}=="067b", ATTRS{idProduct}=="2303", SYMLINK+="imu"
#restart the system 
$sudo udevadm control --reload-rules && udevadm trigger
```

Troubleshooting: 
1. If you do not have the permission to open the serial port:
try to read this article https://websistent.com/fix-serial-port-permission-denied-errors-linux/

Don't forget to add in your bash your catkin sources

```bash
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

# Run

```bash
roslaunch roboteq_control vinebot.launch
```



:rocket: That's it!
