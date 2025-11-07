FDSecure Encryptor APT Repository (FloriDevs)

This repository provides easy installation and automatic updates for the FDSecure Encryptor Java application on Debian and Ubuntu based Linux distributions.

FDSecure Encryptor is a simple, cross-platform tool for password-based file encryption and decryption.

How to Add Our Repository to Your System

Follow these steps to securely add the FloriDevs APT repository and its GPG signing key to your Debian or Ubuntu system. This process prepares your PC for installation but does not install the software yet.

1. Import the GPG Signing Key

To guarantee the authenticity of our packages, you must import the public GPG key used by FloriDevs to sign the repository metadata. We use the modern, secure method (gpg --dearmor) which restricts the key's trust to only this specific repository.

Since direct downloads of the .gpg file can sometimes be challenging, we will download the entire repository as a ZIP archive to ensure you get the key file reliably.

# 1a. Download the repository as a ZIP file from GitHub
# This is a reliable method if the direct link to the .gpg file fails.
wget [https://github.com/FloriDevs/apt-repo-key/archive/refs/heads/main.zip](https://github.com/FloriDevs/apt-repo-key/archive/refs/heads/main.zip)

# 1b. Unzip the file (creates the folder 'apt-repo-key-main')
unzip main.zip

# 1c. Securely import the key and save it to the system keyring
# The 'gpg --dearmor' command converts the key for secure use by APT.
sudo gpg --dearmor -o /usr/share/keyrings/fdsecure-keyring.gpg apt-repo-key-main/FloriDevs-apt-key.gpg

# 1d. Clean up the temporary files and folder
rm -rf main.zip apt-repo-key-main/


2. Add the APT Source

Next, create the configuration file for the repository (.list) in your system's sources directory. This command explicitly links the repository to the securely imported key using the signed-by option.

# 2. Add the repository definition to the APT sources directory
echo "deb [signed-by=/usr/share/keyrings/fdsecure-keyring.gpg arch=all] [https://floridevs.github.io/apt-repo-key](https://floridevs.github.io/apt-repo-key) stable main" | \
  sudo tee /etc/apt/sources.list.d/fdsecure.list > /dev/null


Next Step: updating repo-list

Once the repository and key are successfully added, you have to update your apt repos with following command:

sudo apt update
