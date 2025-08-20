SSH Tunnel
Made by [Hironull]

SSH Tunnel is a simple tool that allows users to install and configure a working SSH server on any VPS. Once installed, you can easily connect to your server using popular SSH clients like Termius, Putty, or the built-in terminal.
✨ Features
📦 One-click SSH installation
🔐 Secure connection setup
🌍 Works with any VPS provider
🖥️ Compatible with Termius, Putty, and OpenSSH clients
⚡ Lightweight and easy to use

🚀 Installation:

1.
apt update && apt install -y git && git clone https://github.com/hironull/ssh-tunnel/ && chmod +x tunnel/tunnel && mv tunnel/tunnel /usr/local/bin/ && rm -rf tunnel && clear

2.
tunnel make 22

🔑 Usage

Once installed, you can connect to your VPS using Termius or any SSH client:
Host: Your VPS IP address
Port: It'll automatically give you an random port
Username: root
Password: Your Vps password

Example command with SSH:

ssh username@your-vps-ip -p yourport
