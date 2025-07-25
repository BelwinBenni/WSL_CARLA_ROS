# TASK 0

Hello there, fellow aspiring autonomous vehicle engineers and enthusiasts! When I first started diving into the world of self-driving cars, it felt a bit overwhelming. But I quickly learned that powerful tools like the CARLA simulator are essential for practice. This guide shares _my personal journey_ in setting up a beginner-friendly CARLA and ROS2 environment on Windows using WSL2, and I hope it helps you kickstart yours too!

This is a step-by-step walkthrough designed to be as straightforward as possible, focusing on a setup that I've found to be reliable and organized for getting CARLA and ROS2 running seamlessly.

### What You'll Need: My System Configuration

Before we begin, you might be wondering about the kind of computer you need. Each software creator prescribes their own minimum requirement, and it's generally good if these are met. However, personally, my system configuration is as follows:

* **Processor:** Intel i5 12th Gen H series
* **RAM:** 16 GB dual channel
* **Graphics Card:** RTX 3050 4GB
* **SSD:** 512GB

With this setup, I am able to run CARLA and ROS with minimal lag, with the CARLA server running on Windows and the CARLA client and ROS running on WSL. This setup has provided a solid and smooth experience, **even though it doesn't meet the bare minimum requirements specified by CARLA**. I believe it's a great example of how you can still make things work for your simulation adventures!

### Task 0: Starting Our Journey with WSL2

Our very first step on this path is to get Windows Subsystem for Linux 2 (WSL2) up and running. Think of WSL2 as a way to have a powerful Linux environment living comfortably right inside your Windows machine. This is crucial because our CARLA client will eventually run here, and ROS2, which we'll cover in a separate guide, thrives in Linux.

1. **Open PowerShell as Administrator:** To begin, search for "PowerShell" in your Windows Start Menu. Once you find it, right-click and select "Run as administrator." This gives us the necessary permissions to install WSL.
2. **Install Ubuntu 22.04 LTS:** In the elevated PowerShell window, type in the following command and press Enter:

```powershell
wsl --install Ubuntu-22.04
```

{% hint style="info" %}
**Why Ubuntu 22.04 LTS specifically?** As a beginner, I found it best to stick with what's most reliable. ROS2 Humble, the version we'll install next, is thoroughly tested and primarily released for Ubuntu 22.04 LTS. While workarounds exist, for a smooth start, I highly recommend this version.
{% endhint %}

1. **Complete Basic Setup:** After the installation finishes, you'll be prompted to set up your new Linux environment. This involves:
   * Providing a **UNIX username** (this will be your username within Ubuntu).
   * Setting a **password** for your new UNIX user. Remember these, as you'll use them often!
2. **Update Your System:** Once you're logged into your fresh Ubuntu environment, it's a good habit (and necessary!) to ensure everything is up to date. Run these commands:

{% code lineNumbers="true" %}
```bash
sudo apt update
sudo apt upgrade -y
```
{% endcode %}

That's it, **Task 0 is done!** Pretty easy! This fetches the latest package information and upgrades your installed software.
