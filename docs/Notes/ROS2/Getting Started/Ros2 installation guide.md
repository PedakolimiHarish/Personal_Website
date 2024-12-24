# Ros2 Installation Guide

How to install ROS2 Jazzy

## Requirement 
Working ubuntu 24.04 LTS, It depends on you how you want to install it like WSL2, VM, Dual Boot or Direct install

## Ros2 Installation

Official setup guild will be available in [Ros2 Jazzy](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html), [automaticaddison jazzy setup](https://automaticaddison.com/how-to-install-ros-2-jazzy/). You follow that too mostly everything is same.

We will begin by installing ROS 2 Jazzy via Debian Packages. Debian packages are software files used to install programs and applications on Ubuntu.

### Setup Locale

Open a new terminal window.

Type this command inside a terminal window.

``` Bash title="Bash"
locale
```

If you see something like this that means you already have locale ready to use, but if you don't then follow along.

``` bash title="Bash"
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

A locale is a set of variables that define the language, country, and character encoding settings. These settings are used by applications to determine how to display text, dates, times, and other information.

Now type the following command:

``` bash title="Bash"
sudo apt update && sudo apt install locales
```

`sudo apt update` updates the package index list. This list is a database of all the software packages available for your version of Ubuntu.

`sudo apt install locales` installs the locales package, which provides support for different languages and regions.

Now type the following commands into the terminal window to generate locale definition files. After each command, press Enter only your keyboard:

``` bash title="Bash"
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

In this case, these commands are generating locale definition files for the English (United States) locale and the English (United States) UTF-8 locale. The UTF-8 locale is a special locale that supports the UTF-8 character encoding, which is the standard encoding for most languages.

Now we need to verify the settings by typing:

``` Bash title="Bash"
locale
```

After installing these you will see the following

``` bash title="Bash"
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

### Enable the Required Repositories

Let’s add the ROS 2 apt repository to our system. APT stands for “Advanced Package Repository”. This repository provides a convenient way to install and manage ROS 2 packages without having to clone packages to your computer from GitHub and build them from that source code.  

Open a terminal window, and type the following two commands:

``` bash title="Bash"
sudo apt install software-properties-common
sudo add-apt-repository universe
```
Press Enter.

The software-properties-common package provides a number of tools for managing software sources on Ubuntu and Debian systems. 

The universe repository is a software repository that contains a wide variety of software packages, including many that are not included in the default Ubuntu and Debian repositories. 

Now we need to add the ROS 2 GPG key with apt. The ROS 2 GPG key makes sure the software packages you are installing are from a trusted source.

Type these two commands:

``` bash title="Bash"
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

Add the repository to your sources list (copy and paste all of this below):

``` bash title="Bash"
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2-testing/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

Type the following command to install ROS 2 development tools.

``` bash title="Bash"
sudo apt update && sudo apt install ros-dev-tools
```

Now update the apt repository:

``` bash title="Bash"
sudo apt update -y
```

Upgrade the packages on your system to make sure you have the newest versions.

``` bash title="Bash"
sudo apt upgrade -y
```

### Install ROS 2
Here is where we get to install ROS 2 Jazzy. 

Open a terminal window, and type this command:

Desktop Install (Recommended): ROS, RViz, demos, tutorials.

``` bash title="Bash"
sudo apt install ros-jazzy-desktop
```

ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.

``` bash title="Bash"
sudo apt install ros-jazzy-ros-base
```

### Set Up the Environment Variables

Once jazzy has finished installing, you need to set up the important environment variables. Environment variables are settings that tell your computer how to find and use ROS 2 commands and packages.

Open a terminal window, and type this command:

``` bash title="Bash"
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
```

When you run this command, it appends the line source `/opt/ros/jazzy/setup.bash` to your `~/.bashrc` file. 

What does this do? Each time you open a new terminal window, you are starting what is called a bash session. The bash session needs to know what version of ROS 2 you are using. 

By adding this line `(echo “source /opt/ros/jazzy/setup.bash”)` to your `~/.bashrc` file, you ensure the necessary environment variables and paths for ROS 2 Jazzy are properly set up each time you open a new terminal window, allowing you to use ROS 2 commands and tools without having to manually run the setup.bash script every time.

For the changes to take effect, you now need to open a new terminal window, or you can type this command in the current terminal:

``` bash title="Bash"
source ~/.bashrc
```

You can verify that line was added by typing:

``` bash title="Bash"
cd
nano .bashrc
```

and at the end you will see 

``` bash title="Bash"
source /opt/ros/jazzy/setup.bash
```
## Install Gazebo and Other Useful Packages

Let’s install some other useful packages like pip (the Python package manager), Gazebo, a simulation software for robotics, and NumPy, a scientific computing library for Python.

``` bash title="Bash"
sudo apt-get install python3 python3-pip -y
sudo apt-get install ros-${ROS_DISTRO}-ros-gz -y
sudo apt-get install python3-numpy
```

Let’s make these environment variables permanent. Open a terminal window, and type these commands, one after the other:

``` bash title="Bash"
echo 'export LIBGL_ALWAYS_SOFTWARE=1' >> ~/.bashrc
echo 'export QT_QPA_PLATFORM=xcb' >> ~/.bashrc
source ~/.bashrc
```

## Test your Gazebo Installation

open a new terminal window, and type:

``` bash title="Bash"
gz sim -v 4 shapes.sdf
```

You should see something like this


<figure markdown="span">
  ![gazebo shapes.sdf](Resources\gazebo_test_01.png)
  <figcaption>gazebo shapes.sdf</figcaption>
</figure>


This command will launch gazebo 
``` bash title="Bash"
gz sim 
```

## Test Your ROS 2 Installation.

Now that we have tested Gazebo, let’s test our ROS 2 installation by running some sample programs.

Open a terminal window, and type:

``` bash title="Bash"
ros2 run demo_nodes_cpp talker
```

<figure markdown="span">
  ![demo_talker](Resources\demo_talker.png)
  <figcaption>demo_talker</figcaption>
</figure>

This command runs a pre-built program called “talker” that comes with ROS 2. The “talker” program publishes messages to the ROS 2 system in string format. 

Open another terminal window, and type:

``` bash title="Bash"
ros2 run demo_nodes_py listener
```
<figure markdown="span">
  ![demo_listener](Resources\demo_listener.png)
  <figcaption>demo_listener</figcaption>
</figure>

If your output looks similar to the images above, you have installed ROS 2 successfully. 

To close these programs, press CTRL + C on your keyboard in both terminal windows.

Now you have installed Ros2 Jazzy and Gazebo Harmonic successfully, now go learn more about ros2.

## Uninstall

If you need to uninstall ROS 2 or switch to a source-based install once you have already installed from binaries, run the following command:

``` bash title="Bash"
sudo apt remove ~nros-jazzy-* && sudo apt autoremove
```

You may also want to remove the repository:

``` bash title="Bash"
sudo rm /etc/apt/sources.list.d/ros2.list
sudo apt update
sudo apt autoremove
# Consider upgrading for packages previously shadowed.
sudo apt upgrade
```
