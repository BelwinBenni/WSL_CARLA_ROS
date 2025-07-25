# Part 2: Installing ROS2 Humble - The Robotics Brain

Welcome to the second part of our beginner's journey! Now, it's time to dive into the powerful robotics framework ROS2 Humble, which will serve as the "brain" for our autonomous applications. After that, we'll install the crucial CARLA-ROS2 bridge to connect everything.

We'll be using the official Debian package provided by the ROS team for ROS2, which is the most recommended and stable way for beginners to install it.

1. **Enable Ubuntu Universe Repository:** First, let's make sure an important Ubuntu repository is enabled. This "Universe" repository contains a lot of open-source software that ROS2 might depend on.

```bash
sudo add-apt-repository universe
```

**Set up Locale (Crucial for ROS):** This step is really important to prevent potential issues with ROS tools later on. It ensures your system's language settings are correctly configured for ROS.

{% code lineNumbers="true" %}
```bash
sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```
{% endcode %}

**Add ROS2 Repository and Key:** Now we'll add the ROS2 repository to your system's list of software sources and add the GPG (GNU Privacy Guard) key to ensure the packages we download are authentic.

{% code overflow="wrap" lineNumbers="true" %}
```bash
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F"'"'{print $4}')
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo $VERSION_CODENAME)_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.deb
```
{% endcode %}

**Update and Install ROS2 Desktop:** After adding the repository, it's time to update your package lists and install the full ROS2 Desktop environment. This includes not just the core ROS libraries but also tools like RViz (for 3D visualization) and other common development utilities that are incredibly useful for robotics.

{% code lineNumbers="true" %}
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install ros-humble-desktop -y
```
{% endcode %}

{% hint style="info" %}
This particular step might take a little while, depending on your internet connection, so grab a coffee or take a short break!
{% endhint %}

#### Configuring ROS2 Environment Variables

To make sure ROS2 commands are available every time you open a new terminal, we'll set up environment variables in `/etc/profiles.d`. This is a clean way to automatically source the ROS2 setup script without cluttering your `~/.bashrc`.

**Create the `ros2.sh` script:**

```bash
sudo nano /etc/profiles.d/ros2.sh
```

**Add the following content to the file:**

{% code title="ros2.sh" %}
```sh
if [ -d "/opt/ros/humble" ]; then
    source /opt/ros/humble/setup.sh
fi
```
{% endcode %}

Save the file (Ctrl+O, Enter) and exit nano (Ctrl+X).

**Make the script executable:**

```bash
sudo chmod +x /etc/profiles.d/ros2.sh
```

Now, close and reopen your WSL terminal. ROS2 commands should be available!

