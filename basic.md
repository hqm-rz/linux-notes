### Server List & Quick Info

| No | Hostname & Distro                            | Kernel + Arch                          | Disk Usage                          | Services Status                                      |
|----|----------------------------------------------|----------------------------------------|-------------------------------------|------------------------------------------------------|
| 1  | **Ubuntu 24.04 LTS**<br>`prod-web01`         | `6.8.0-51-generic x86_64`              | <code>df -h /</code><br>`35% used`  | nginx 🟢 mysql 🟢 redis 🟢 fail2ban 🟢                |
| 2  | **Debian 12 Bookworm**<br>`db01`             | `6.1.0-26-amd64 x86_64`                | <code>df -h /</code><br>`62% used`  | mariadb 🟢 postgres 🟢 docker 🟢                       |
| 3  | **AlmaLinux 9.5**<br>`backup01`              | `5.14.0-427.el9.x86_64`                | <code>df -h /backup</code><br>`81% used` | rsync 🟢 borg 🟢 restic 🟢                     |
| 4  | **Arch Linux**<br>`dev-box`                  | `6.11.2-arch1-1 x86_64`                | <code>df -h /</code><br>`18% used`  | podman 🟢 nvim 🟢 zsh 🟢                             |

#### Useful commands (click to copy)

```bash
# Info sistem
cat /etc/os-releaselsb_release -a || cat /etc/os-release
