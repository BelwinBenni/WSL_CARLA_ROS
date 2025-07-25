# Part 3: Installing the CARLA ROS2 Bridge

This is where the magic happens – connecting your ROS2 world with your CARLA simulator! We'll download and build the `carla-ros-bridge` from its repository.

**Navigate to `/opt` and clone the bridge repository:**

{% code overflow="wrap" lineNumbers="true" %}
```bash
cd /opt
sudo git clone --recurse-submodules https://github.com/ttgamage/carla-ros-bridge.git
```
{% endcode %}

{% hint style="info" %}
Using `--recurse-submodules` is important as the bridge might depend on other sub-projects.
{% endhint %}

**Install `colcon` and `rosdep`:** These are essential tools for building ROS2 packages and managing their dependencies.

```bash
sudo apt install python3-colcon-core python3-rosdep2 -y
```

**Update `rosdep` and install dependencies:** `rosdep` helps you find and install system dependencies for ROS packages.

{% code lineNumbers="true" %}
```bash
rosdep update
rosdep install --from-paths carla-ros-bridge --ignore-src -r
```
{% endcode %}

**Build the CARLA ROS2 Bridge:** Finally, we use `colcon` to build the bridge. This compiles the code and sets up the necessary files for ROS2 to recognize and use it.

{% code lineNumbers="true" %}
```bash
cd /opt/carla-ros-bridge
colcon build
```
{% endcode %}

{% hint style="info" %}
This `colcon build` command might take some time, as it compiles all the components of the bridge.
{% endhint %}

And just like that, you've reached another significant milestone in your autonomous vehicle journey! You've now successfully installed ROS2 Humble and the crucial CARLA ROS2 Bridge. Your environment is fully set up for you to start integrating the "brain" (ROS2) with the "body" (CARLA simulator)!
