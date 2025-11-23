# Clone Git Repo via SSH in WSL (Windows Subsystem for Linux)

Step-by-step guide to set up SSH keys in WSL and clone Git repositories without password.

### Step 1: Open WSL
```bash
wsl
# or specific distro
wsl -d Ubuntu
```

### Step 2: Check version
```bash
lsb_release -a
```

### Step 3: Check if there any ssh key were there before 
```bash
ls -al ~/.ssh
```

### Step 4: Generate Key
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Step 5: Copy the public key
```bash
cat ~/.ssh/id_ed25519.pub | clip.exe
```

### step 6: Put key to github
```bash
GitHub → Settings → SSH and GPG keys → New SSH key → paste
```

### Step 7: Run SSH Agent
```bash
nano ~/.bashrc
```

### Step 8: Run this
```bash
echo -e "\n# ==== WSL SSH Agent Auto Start ====\nif [ -z \"\$SSH_AUTH_SOCK\" ]; then\n    eval \"\$(ssh-agent -s)\" > /dev/null\n    ssh-add ~/.ssh/id_ed25519 2>/dev/null\nfi" >> ~/.bashrc && source ~/.bashrc && echo "Done! SSH agent will start automatically now."
```

### Step 9: Save file
```bash
press Ctrl + X
```

### Step 10: Apply Changes
```bash
source ~/.bashrc
```

### Step 11: SSH connection test
```bash
ssh -T git@github.com
```

### Step 12: Change directory
```bash
cd /d E:\Laravel\Laravel_Projects
```

### Step 13: Clone Repository
```bash
git clone git@github.com:username/repository.git
```
