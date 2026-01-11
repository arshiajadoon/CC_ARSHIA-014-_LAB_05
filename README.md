# Package Management Lab 5 - Cloud Computing

**Student:** Arshia Jadoon  
**Registration:** BSE-2023-014

## Overview

Linux package management, GUI installation, and vim editor mastery - covering apt, snap, PPAs, and advanced text editing.

---

## Tasks Completed

### Task 1: Java Installation with apt
```bash
sudo apt install default-jdk    # Install Java
java --version                  # Verify installation
sudo apt remove default-jdk     # Remove Java
java                           # Command not found
hash -r                        # Clear command cache
```

### Task 2: Java with apt-get
```bash
sudo apt-get install default-jdk
java --version
sudo apt-get remove default-jdk
hash -r
```

### Task 3: apt update vs apt upgrade
```bash
sudo apt update     # Update package lists
sudo apt upgrade    # Upgrade installed packages
```

**Difference:**
- `apt update` - Refreshes package index (doesn't install)
- `apt upgrade` - Installs newer versions of packages
- Always run `update` before `upgrade`

### Task 4: VS Code via Snap
```bash
sudo snap install code --classic
snap list
code --version
which code                      # /snap/bin/code
```
✅ **Do NOT remove VS Code**

### Task 5: XFCE Desktop + XRDP
```bash
sudo apt update
sudo apt install xfce4 xfce4-goodies
sudo apt install xrdp
sudo systemctl enable xrdp
sudo systemctl status xrdp
echo xfce4-session > ~/.xsession
```
✅ Connected via RDP  
✅ Launched VS Code in GUI  

### Task 6: LightDM Display Manager
```bash
sudo apt install lightdm lightdm-gtk-greeter
sudo dpkg-reconfigure lightdm
sudo systemctl enable lightdm   # Enable GUI on boot
sudo reboot
sudo systemctl disable lightdm  # Disable GUI on boot
sudo systemctl start lightdm    # Start GUI manually
sudo systemctl stop lightdm     # Stop GUI
```

### Task 7: Google Chrome Installation

**Method 1: Manual sources.list**
```bash
sudo nano /etc/apt/sources.list
# Add: deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo apt update
sudo apt install google-chrome-stable
```

**Method 2: Separate .list file (Recommended)**
```bash
echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | \
  sudo tee /etc/apt/sources.list.d/google-chrome.list
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo apt update
sudo apt install google-chrome-stable
```

### Task 8: PPAs (Audacity & OBS)

**Audacity:**
```bash
sudo add-apt-repository ppa:ubuntuhandbook1/audacity
sudo apt update
sudo apt install audacity
audacity
```

**OBS Studio:**
```bash
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install obs-studio
obs
```

### Task 9: Kubernetes YAML with vim
```bash
vim --version
sudo apt install vim           # If needed
mkdir -p ~/k8s-lab
cd ~/k8s-lab
vim k8s-sample.yaml
```

**Sample YAML:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

### Task 10: Edit & Verify YAML
```bash
vim k8s-sample.yaml
# Add annotation in metadata section
# Verify changes
# Discard temporary edits with :q!
```

### Task 11: vim Editing Practice
```
dd          # Delete line
u           # Undo
3dd         # Delete 3 lines
gg          # Go to first line
G           # Go to last line
:5          # Go to line 5
```

### Task 12: vim Search & Replace
```
/nginx      # Search for "nginx"
n           # Next match
N           # Previous match
:%s/nginx/apache/g   # Replace all nginx with apache
u           # Undo
:q!         # Quit without saving
```

---

## Package Management Overview

### apt vs apt-get

| Feature | apt | apt-get |
|---------|-----|---------|
| User-friendly | ✅ Yes | ❌ No |
| Progress bar | ✅ Yes | ❌ No |
| Colored output | ✅ Yes | ❌ No |
| Recommended for | Interactive use | Scripts |

### Common Commands

**apt/apt-get:**
```bash
sudo apt update              # Update package lists
sudo apt upgrade             # Upgrade packages
sudo apt install <pkg>       # Install package
sudo apt remove <pkg>        # Remove package
sudo apt purge <pkg>         # Remove with config
sudo apt autoremove          # Remove unused packages
apt search <pkg>             # Search packages
apt show <pkg>               # Show package info
```

**snap:**
```bash
sudo snap install <pkg>      # Install snap package
sudo snap remove <pkg>       # Remove snap
snap list                    # List installed snaps
snap find <pkg>              # Search snaps
```

**PPA:**
```bash
sudo add-apt-repository ppa:<name>    # Add PPA
sudo apt update                       # Update after adding
sudo add-apt-repository --remove ppa:<name>  # Remove PPA
```

---

## vim Cheat Sheet

### Modes
- **Normal mode** - Navigation and commands (press `Esc`)
- **Insert mode** - Type text (press `i`, `a`, `o`)
- **Visual mode** - Select text (press `v`)
- **Command mode** - Execute commands (press `:`)

### Basic Commands

**Entering Insert Mode:**
```
i           # Insert before cursor
a           # Append after cursor
o           # Open new line below
O           # Open new line above
```

**Navigation:**
```
h j k l     # Left, down, up, right
w           # Next word
b           # Previous word
0           # Start of line
$           # End of line
gg          # First line
G           # Last line
:n          # Go to line n
```

**Editing:**
```
x           # Delete character
dd          # Delete line
yy          # Copy line
p           # Paste
u           # Undo
Ctrl+r      # Redo
```

**Search & Replace:**
```
/pattern    # Search forward
?pattern    # Search backward
n           # Next match
N           # Previous match
:%s/old/new/g       # Replace all
:%s/old/new/gc      # Replace with confirmation
```

**Save & Quit:**
```
:w          # Save
:q          # Quit
:wq         # Save and quit
:q!         # Quit without saving
ZZ          # Save and quit (Normal mode)
```

---

## GUI Setup Summary

### XFCE Desktop Environment
- Lightweight desktop environment
- Good for VMs and remote access
- Includes basic applications

### XRDP (Remote Desktop)
- RDP server for Linux
- Connect from Windows Remote Desktop
- Port 3389 (default)

### LightDM (Display Manager)
- Login screen manager
- Can enable/disable GUI on boot
- Switch between GUI and CLI

---

## Package Sources

### APT Sources
**Location:** `/etc/apt/sources.list` and `/etc/apt/sources.list.d/`

**Format:**
```
deb [arch=amd64] http://example.com/repo focal main
│   │            │                   │     │
│   │            │                   │     └─ Component
│   │            │                   └─────── Release
│   │            └─────────────────────────── Repository URL
│   └──────────────────────────────────────── Architecture
└──────────────────────────────────────────── Package type
```

### GPG Keys
- Verify package authenticity
- Required for third-party repos
- Add with `apt-key add` or newer methods

---

## Troubleshooting

**Package conflicts:**
```bash
sudo apt --fix-broken install
sudo dpkg --configure -a
```

**Hash cache issues:**
```bash
hash -r                      # Clear bash command cache
```

**Snap not working:**
```bash
sudo snap refresh            # Update snapd
sudo systemctl restart snapd # Restart service
```

**GUI won't start:**
```bash
sudo systemctl status lightdm
sudo systemctl restart lightdm
```

**vim not installed:**
```bash
sudo apt install vim
```

---

## Best Practices

✅ Always `apt update` before `apt upgrade`  
✅ Use `apt` for interactive, `apt-get` for scripts  
✅ Prefer official repos over PPAs when possible  
✅ Remove unused packages with `autoremove`  
✅ Keep system updated regularly  
✅ Use snap for self-contained applications  
✅ Practice vim regularly for proficiency  

---

## Learning Outcomes

✅ Install/remove packages with apt and snap  
✅ Understand package management hierarchy  
✅ Add third-party repositories (PPAs)  
✅ Install and configure GUI environments  
✅ Use vim for efficient text editing  
✅ Search and replace with vim  
✅ Manage display managers  
✅ Configure remote desktop access  

---

## Resources

- [Ubuntu Packages](https://packages.ubuntu.com/)
- [Snap Store](https://snapcraft.io/store)
- [Vim Adventures](https://vim-adventures.com/) - Learn vim by playing
- [Vim Cheat Sheet](https://vim.rtorr.com/)

---

## Author

**Arshia Jadoon**  
BSE-2023-014  
Semester VA

---

*Lab 5 - Cloud Computing Course
