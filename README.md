# UAVHooper

## Installing the simulator

### Parrot Sphinx

Follow the instructions at the documentation on adding and installing the required packages and go through the first steps. 

https://developer.parrot.com/docs/sphinx/installation.html

In short, for ubuntu 18.04, these are the commands

```bash
$ echo "deb http://plf.parrot.com/sphinx/binary `lsb_release -cs`/" | sudo tee /etc/apt/sources.list.d/sphinx.list > /dev/null
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 508B1AE5
$ sudo apt update
$ sudo apt install parrot-sphinx
```

Add your user to the sphinx group and relog to apply the changes.

firmared will be needed for every simulation. Either register it to start with the system or remember to start it manualy

```bash
$ sudo systemctl start firmwared.service
$ sudo systemctl register firmwared.service
```

check the service with:

```bash
$ fdc ping
```
You should get

```bash
PONG
```

### Check your wifi interface name
You will need to remember this interface to pass it onto the simulation launch file

```bash
$ iwconfig
```

```bash
$ sphinx /opt/parrot-sphinx/usr/share/sphinx/drones/anafi4k.drone::stolen_interface=<your_interface_name>:eth0:192.168.42.1/24
```

## Connecting to ROS

To connect to the drone we will need the bebop_autonomy package

add the following repository to your ROS workspace
 
```bash
$ git clone https://github.com/AutonomyLab/bebop_autonomy.git
```

Install the dependencies and build the package

```bash
rosdep install --from-paths src -i
catkin build
```

On Ubuntu 18.04, the libbebop_driver_nodelet.so will not be configured properly as it is located inside the `/opt/ros/melodic/lib/parrot_arsdk` directory and was not installed correctly onto the catkin_ws. 

A quick workaround is to add `/opt/ros/melodic/lib/parrot_arsdk` to `$LD_LIBRARY_PATH`. or just copy all the files in there to your `<WORKSPACE_FOLDER>/devel/lib/`


## Utilizing bebop_autonomy

If needed, you can find more in-depth instructions on how to utilize the package the following repository:

https://github.com/Insper/bebop_sphinx/blob/master/docs/instrucoes_sphinx.md#bebop_autonomy

## Refs
 - https://www.ics.uci.edu/~chaow17/research/urop.pdf

 - http://www.ahmedahres.com/blog/detection-of-a-hula-hoop-using-computer-vision

