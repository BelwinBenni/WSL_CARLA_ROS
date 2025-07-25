# Part 1: Setting Up CARLA on WSL2

Now that WSL2 and Ubuntu are ready, let's prepare our development environment by installing some core tools and simultaneously get CARLA downloading.

**Install Core Tools:** In your WSL2 Ubuntu terminal, run this command. These are fundamental tools that we'll rely on throughout our setup:

{% code overflow="wrap" %}
```bash
sudo apt install -y curl wget gnupg2 git unzip build-essential software-properties-common ca-certificates lsb-release apt-transport-https python-is-python3 python3-pip
```
{% endcode %}

> This will install the primary tools we require on the system. While these essential tools are being installed, let's switch back to Windows and get CARLA downloading!

**Download CARLA 0.9.15:** On your Windows machine, open your web browser and navigate to the official CARLA website. Look for and download **CARLA\_0.9.15** for Windows.

> **A Personal Note on Maps:** My system, with its RTX 3050 4GB graphics card, handles simulations best with lightweight maps. I personally stick to **TOWN 02** for smooth performance. If your system is designed for running full CARLA, feel free to download the additional maps as well. It's all about finding what works best for your hardware!

> #### Organizing Our Workspace (My Approach to Keeping Things Tidy!)

{% hint style="info" %}
As our CARLA download continues, let's prepare our workspace. Every person is unique; hence, everyone has a different preference and setup choice. Personally, I like to keep my system clean, organized, and modular. So, rather than throwing files and folders around, I prefer keeping them in their designated spaces. I can understand that it will differ on a personal level, so if your installation and setup directories are different, then modify the commands accordingly.
{% endhint %}

{% hint style="info" %}
**CARLA Root Directory:** I prefer to extract and keep the CARLA files in my `D:` drive. So, for me, the CARLA server root will be `D:\CARLA_0.9.15\WindowsNoEditor`. Throughout this guide, when you see `<CARLA_ROOT_PATH>`, that's where you'll substitute your actual CARLA folder location.
{% endhint %}

{% hint style="info" %}
**Python Environment:** For Python, I prefer using the bundled version with Ubuntu-22.04, and instead of Anaconda, I will be using `virtualenvwrapper`. As it adheres to my ideology of keeping things simple and minimal, giving me greater control over my machine and tools.
{% endhint %}

#### Copying CARLA's PythonAPI to WSL

After CARLA has finished downloading, extract it to your `D:` drive and navigate to the `D:\CARLA_0.9.15\WindowsNoEditor` folder. In that, locate a folder named `PythonAPI`. We need to move this folder to WSL so our Linux-based Python scripts can interact with CARLA.

1. **Create a CARLA directory in WSL:** In your WSL Ubuntu terminal, run this command to create a dedicated space for CARLA-related files:

{% code lineNumbers="true" %}
```bash
cd ~
mkdir CARLA
```
{% endcode %}

**Copy the PythonAPI folder:** From your WSL terminal, you can use the `cp` command. Make sure to replace `/mnt/d/CARLA_0.9.15/WindowsNoEditor` with the actual path where you extracted CARLA on your Windows drive:

```bash
cp -r /mnt/d/CARLA_0.9.15/WindowsNoEditor/PythonAPI CARLA
```

#### Testing Our CARLA Simulator Setup

It's always a good idea to test things out before moving on! Let's verify that CARLA is working correctly.

1. **Launch CARLA Server (on Windows):** On your Windows machine, go to your `<CARLA_ROOT_PATH>` (e.g., `D:\CARLA_0.9.15\WindowsNoEditor`). Open **Terminal** in this directory (or PowerShell) by right-clicking and selecting "Open in Terminal". Execute the command:

```powershell
.\CarlaUE4.exe -vulkan
```

{% hint style="info" %}
_Remember to replace `D:\CARLA_0.9.15\WindowsNoEditor\` with your actual CARLA root path._
{% endhint %}

If it ran successfully, the CARLA simulator window will pop up. This will launch the CARLA server using the Vulkan rendering API, which can be more efficient for some systems, especially if your graphics card doesn't meet the bare minimum VRAM requirements (like a 4GB card).

{% hint style="warning" %}
**Crucial WSL Networking Tip (Learned the Hard Way!):** This is super important and something I discovered after much troubleshooting! For your WSL client to connect to the CARLA server, your WSL networking mode _must_ be set to **mirrored**. If it's not, you'll likely face connectivity issues.

I learned this the hard way after many failed attempts. When other AI tools and common troubleshooting steps didn't work, I had an "aha!" moment and remembered a failed experiment from about five years ago. That old experience gave me the idea that this networking configuration might be the problem. Once I changed the mode of WSL networking to mirrored, it worked perfectly!

To configure this, you need to open your WSL settings. You can usually find these in the Windows Start Menu by searching for "Windows Subsystem for Linux" or directly modifying the `.wslconfig` file. Inside the settings (or `.wslconfig`), ensure that the networking mode is set to "mirrored." This allows CARLA in Windows and your WSL environment to communicate seamlessly, preventing those frustrating connection failures. This was a critical fix for me after trying everything else!
{% endhint %}

**Run Manual Control from WSL:** Now, switch back to your WSL Ubuntu terminal. We'll navigate into the `PythonAPI` folder we just copied and run an example script to control a car manually:

{% code lineNumbers="true" %}
```bash
cd ~/CARLA/PythonAPI/examples
python3 manual_control.py
```
{% endcode %}

If everything is set up correctly, the CARLA simulator window on your Windows machine should connect to this client. You should then be able to use the **W, A, S, D, E** keys to navigate around the virtual map. Play around for a bit to verify it's working! Once you're done, you can close both the CARLA simulator window and the `manual_control.py` script (press `Ctrl+C` in your WSL terminal).

Congratulations! You've successfully set up the CARLA simulator on your Windows machine and connected to it from WSL2. This is a huge step in your autonomous vehicle journey! Now that your simulation environment is ready, you're prepared for the next part: getting the "brain" of your robotics applications installed.
