# SSH Auto-login Setup Guide

This repository provides a guide and resources on setting up automatic login to remote servers using SSH and key pairs, which simplifies the process of logging into remote machine. The following can be done using a MacOS or Linux OS device.

## ⚠️ Security Warning ##


Setting up passwordless SSH authentication to your Tux account significantly streamlines your workflow by allowing you to access your account without manual password input. However, this convenience comes with security implications:

1. **Device Security**: If your local device falls into the wrong hands, they could potentially gain unrestricted access to your Tux account. It is crucial to secure your device with a strong password and consider using full disk encryption. Furthermore, ensure that your device automatically locks after a period of inactivity.
2. **Shared Device Caution**: If your device is shared with others, remember they could also gain access to your Tux account through this setup. Be mindful of who has physical or remote access to your device.
3. **Malware Threats**: If your local device gets infected with malware, an attacker could potentially steal your private SSH keys and gain access to your Tux account. Regularly scan your device for malware using reliable security software.
4. **Public/Private Key Pair Protection**: Your private key should be kept secure at all times, and your public key should only be installed on systems where you need SSH access. Never share your private key.
5. **Account Lock**: In case of any suspicious activity on your Tux account, contact Drexel's IT support immediately to lock the account.
