# Installing Asterisk 22.2.0 on Ubuntu 22.04.2

This guide walks you through installing Asterisk, a powerful open-source PBX system, on a fresh installation of Ubuntu 22.04.2.

## Step 1: Prepare Your System

1.  **Fresh Ubuntu Installation:** Ensure you have a clean installation of Ubuntu 22.04.2 Server.

2.  **Update and Upgrade:** Open a terminal and run these commands to update the package lists and upgrade existing packages:

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

    This ensures you have the latest versions of software, security, and linux kernals.

3.  Install essentials:

    ```bash
     sudo apt install wget build-essential git subversion -y
    ```

4.  (Optional) Install DAHDI and LibPRI for analog lines or ISDN (WIP Need Help):

    Download Tarballs

    ```bash
    cd ~
    wget https://downloads.asterisk.org/pub/telephony/dahdi-linux-complete/dahdi-linux-complete-current.tar.gz
    wget https://downloads.asterisk.org/pub/telephony/libpri/libpri-1-current.tar.gz
    ```

## Step 2: Download & Install Asterisk

1.  **Navigate to Home Directory:** In the terminal, go to your home directory:

    ```bash
    cd ~
    ```

2.  **Download Asterisk Source:** Download the Asterisk 22.2.0 source code from the official Asterisk website:

    ```bash
    wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-22.2.0.tar.gz
    ```

3.  **Extract the Archive:** Extract the downloaded archive using the following command:

    ```bash
    tar -xvzf asterisk-22.2.0.tar.gz
    ```

    This creates a directory named `asterisk-22.2.0` in your home directory.

4.  **Navigate to Asterisk Directory:** Go into the extracted Asterisk directory:

    ```bash
    cd asterisk-22.2.0
    ```

5.  **Install Asterisk Dependencies:**

    ```bash
    sudo contrib/scripts/install_prereq install
    ```

    This script attempts to automatically install the required dependencies.

6.  **Make and Install:**

    ```bash
    sudo ./configure
    ```

    If all dependencies are install, and ./configure was successful, you'll see the Asterisk ASCII art

    ```bash
    sudo make menuselect
    ```

    Enable / Disable modules - Default is fine

    ```bash
    sudo make
    ```

    ```bash
    sudo make install
    ```

    Installs the Asterisk system

7.  **(Optional) Make Samples, Documentation, and Startup:**

    ```bash
    sudo make samples
    ```

    Generates sample files to use to get started

    ```bash
    sudo make progdocs
    ```

    Generates asterisk program documentation

    ```bash
    sudo make config
    ```

    Makes Asterisk boot automatically at startup

8.  **Start & Verify Asterisk System**

    ```bash
    sudo systemctl start asterisk
    ```

    Starts Asterisk daemon

    ```bash
    sudo systemctl status asterisk
    ```

    Checks the status of the Asterisk daemon
    Note: You may see a radius error, this can be ignored.
