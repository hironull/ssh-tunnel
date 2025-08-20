# SSH Tunnel

A small, lightweight tool to install and configure a working SSH server on a VPS quickly. Designed to get a secure SSH endpoint up and running and give you a port to connect with common clients such as Termius, PuTTY, or OpenSSH.

> NOTE: This tool requires root (or sudo) access on the VPS. Use responsibly and only on machines you own or administer.

## Features
- One-command installation
- Simple port setup (can use a specified port or a randomized high port)
- Compatible with Termius, PuTTY and OpenSSH clients
- Minimal, lightweight binary

## Table of contents
- Installation
- Quick start
- Usage examples

---

## Installation

Run these commands on your VPS (Debian/Ubuntu-compatible example):

```bash
sudo apt update
sudo apt install -y git
git clone https://github.com/hironull/ssh-tunnel.git
chmod +x ssh-tunnel/tunnel
sudo mv ssh-tunnel/tunnel /usr/local/bin/tunnel
rm -rf ssh-tunnel
clear
```

This will place the `tunnel` binary into `/usr/local/bin` for easy use.

---

## Quick start

Create an SSH configuration (example uses port 22 as argument):

```bash
sudo tunnel make 22
```

- If you pass a port, the tool will attempt to configure that port.
- If you omit the port, the tool may select and display a randomly chosen high port for use.

After the command completes, the tool will print the connection details (host IP, port, username). Example output:

Host: <your-vps-ip>
Port: <assigned-port>
Username: root
Password: <your-vps-password>

To connect from your machine:

```bash
ssh root@your-vps-ip -p <assigned-port>
```

(or configure Termius / PuTTY with the same Host/IP and Port)

---

## Usage examples

- Create or enable SSH on port 2222:
  ```bash
  sudo tunnel make 2222
  ```

- Run without specifying a port (tool may choose a random high port and display it):
  ```bash
  sudo tunnel make
  ```

---

## Security recommendations (must read)

- Change the root password immediately after installation:
  ```bash
  passwd
  ```
- Prefer SSH key authentication and disable password authentication in `/etc/ssh/sshd_config`:
  - Set `PasswordAuthentication no`
  - Set `PermitRootLogin no` (or `without-password`/`prohibit-password` depending on your policy)
  - Restart SSH: `sudo systemctl restart sshd`
- Restrict access with a firewall (ufw example):
  ```bash
  sudo ufw allow <assigned-port>/tcp
  sudo ufw enable
  ```
- Install and configure fail2ban to reduce brute-force risk.
- Regularly update the system: `sudo apt update && sudo apt upgrade -y`

---

## Uninstall / Cleanup

If you installed the binary to `/usr/local/bin`:

```bash
sudo rm -f /usr/local/bin/tunnel
```

Also undo any SSH configuration changes you no longer want and remove firewall rules you added.

---

## Troubleshooting

- If SSH doesn't start after configuring a new port:
  - Check `sudo journalctl -u sshd -n 200` for errors.
  - Make sure port is not in use: `sudo ss -tuln | grep <port>`
  - Verify `/etc/ssh/sshd_config` syntax: `sshd -t`
- If you are locked out, use your VPS provider's console/serial access to regain access.

---

## Contributing

Contributions, bug reports, and suggestions are welcome. Open an issue or submit a pull request on the repository.

---

## License

Specify a license for the project (e.g., MIT). If you don't have one yet, add a LICENSE file.

---
