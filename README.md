# Beginner's Guide: Installing Asterisk 22.2.0 on Ubuntu 22.10

This guide walks you through installing Asterisk, a powerful open-source PBX system, on a fresh installation of Ubuntu 22.10.

## Step 1: Prepare Your System

1.  **Fresh Ubuntu Installation:** Ensure you have a clean installation of Ubuntu 22.10 Server (or Desktop). This minimizes potential conflicts.

2.  **Update and Upgrade:** Open a terminal and run these commands to update the package lists and upgrade existing packages:

    ```bash
    sudo apt update
    sudo apt upgrade
    ```

    This ensures you have the latest versions of software and security updates.

## Step 2: Download Asterisk

1.  **Navigate to Home Directory:** In the terminal, go to your home directory:

    ```bash
    cd ~
    ```

2.  **Download Asterisk Source:** Download the Asterisk 22.2.0 source code from the official Asterisk website:

    ```bash
    wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-22.2.0.tar.gz
    ```

## Step 3: Extract Asterisk

1.  **Extract the Archive:** Extract the downloaded archive using the following command:

    ```bash
    tar -xvzf asterisk-22.2.0.tar.gz
    ```

    This creates a directory named `asterisk-22.2.0` in your home directory.

## Step 4: Configure and Install Dependencies

1.  **Navigate to Asterisk Directory:** Go into the extracted Asterisk directory:

    ```bash
    cd asterisk-22.2.0
    ```

2.  **Run the Configure Script:** Execute the `configure` script to prepare the build environment:

    ```bash
    ./configure
    ```

3.  **Resolve Dependencies (If Necessary):** If the `configure` script fails due to missing dependencies, you can use the provided script to install them. Run:

    ```bash
    sudo ./contrib/scripts/install_prereq install
    ```

    This script attempts to automatically install the required dependencies.

4.  **Re-run Configure:** After resolving any dependencies, re-run the `configure` script:

    ```bash
    ./configure
    ```

    It should now complete without errors.

## Step 5: Configure Asterisk Modules

1.  **Run `make menuselect`:** This command provides a text-based interface to select which Asterisk modules you want to install:

    ```bash
    make menuselect
    ```

2.  **Select Modules:**

    *   Use the arrow keys to navigate the menu.
    *   Press the `Enter` key to select or deselect modules.
    *   Pay special attention to the `Codec Translators` and `Channel Drivers` sections. Select the codecs and channel drivers appropriate for your setup (e.g., `chan_sip` for SIP, `codec_ulaw` and `codec_alaw` for common audio codecs).

3.  **MP3 Support (Optional):** If you selected MP3 support, you'll need to run a separate script *after* the `make install` step (Step 8):

    ```bash
    contrib/scripts/get_mp3_source.sh
    ```

## Step 6: Compile and Install Asterisk

1.  **Compile Asterisk:** Run the `make` command to compile the Asterisk source code:

    ```bash
    make
    ```

    This process can take a while, depending on your system's hardware.

2.  **Install Asterisk:** Install Asterisk using the following command:

    ```bash
    sudo make install
    ```

    This copies the compiled binaries and libraries to their appropriate locations.

## Step 7: Install Sample Configuration Files and Documentation

1.  **Install Sample Configuration Files:** Install sample configuration files using:

    ```bash
    sudo make samples
    ```

    These sample files provide a good starting point for configuring your Asterisk system.

2.  **Install Program Documentation:** Install program documentation using:

    ```bash
    sudo make progdocs
    ```

3.  **Configure File Permissions:** Ensure correct file permissions using:

    ```bash
    sudo make config
    ```

## Step 8: (If MP3 Selected) Install MP3 Codec

1.  **Get the MP3 Source**:
    ```bash
    contrib/scripts/get_mp3_source.sh
    ```
2.  Follow directions

## Step 9: Start Asterisk

1.  **Start Asterisk:** Start the Asterisk service using:

    ```bash
    sudo systemctl start asterisk
    ```

    (The older `/etc/init.d/asterisk start` method might still work, but `systemctl` is the preferred method on modern Ubuntu systems.)

2.  **Check Asterisk Status:** Verify that Asterisk is running with:

    ```bash
    sudo systemctl status asterisk
    ```

    (Again, the older `/etc/init.d/asterisk status` might work, but `systemctl` is preferred.)

## Step 10: Access the Asterisk CLI

1.  **Connect to the CLI:** Connect to the Asterisk command-line interface (CLI) using:

    ```bash
    sudo asterisk -rvvvvv
    ```

    The `-r` flag connects to a running Asterisk instance. The `vvvvv` increases the verbosity (debugging information).

## Step 11: Configure Asterisk (Important!)

1.  **Configuration Directory:** The main Asterisk configuration files are located in the `/etc/asterisk/` directory.

    ```bash
    cd /etc/asterisk/
    ```

2.  **Edit Configuration Files:** Use a text editor (e.g., `nano`, `vim`) to edit the configuration files (e.g., `sip.conf`, `extensions.conf`) to set up your SIP trunks, extensions, dial plan, and other settings. *This is where you'll customize Asterisk to fit your specific needs.*

## Important Notes:

*   **Permissions:** Ensure you use `sudo` when required for commands that need administrative privileges.
*   **Firewall:** Configure your firewall to allow SIP (port 5060 UDP and TCP), RTP (ports defined in `rtp.conf`), and any other necessary ports.
*   **Documentation:** Refer to the official Asterisk documentation for detailed information on configuration options and applications:  [https://www.asterisk.org/documentation/](https://www.asterisk.org/documentation/)
*   **Security:** Pay close attention to security. Use strong passwords, enable encryption (TLS), and configure your firewall to protect your Asterisk system.
