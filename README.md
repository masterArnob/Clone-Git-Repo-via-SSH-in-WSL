# Clone Git Repo via SSH in WSL (Windows Subsystem for Linux)

Step-by-step guide to set up SSH keys in WSL and clone Git repositories without password.

### Step 1: Open WSL
```bash
wsl
# or specific distro
wsl -d Ubuntu
```

### Step 2: Check if there any ssh key were there before 
```bash
ls -al ~/.ssh
```

### Step 3: Generate Key
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Step 4: Copy the public key
```bash
cat ~/.ssh/id_ed25519.pub | clip.exe
```

### step 5: Put key to github
```bash
GitHub → Settings → SSH and GPG keys → New SSH key → paste
```

### Step 6: Run SSH Agent
```bash
nano ~/.bashrc
```

### Step 7: Run this
```bash
echo -e "\n# ==== WSL SSH Agent Auto Start ====\nif [ -z \"\$SSH_AUTH_SOCK\" ]; then\n    eval \"\$(ssh-agent -s)\" > /dev/null\n    ssh-add ~/.ssh/id_ed25519 2>/dev/null\nfi" >> ~/.bashrc && source ~/.bashrc && echo "Done! SSH agent will start automatically now."
```

### Step 8: Save file
```bash
press Ctrl + X
```

### Step 9: Apply Changes
```bash
source ~/.bashrc
```

### Step 7: SSH connection test
```bash
ssh -T git@github.com
```

### Step 8: Change directory
```bash
cd /d E:\Laravel\Laravel_Projects
```

### Step 9: Clone Repository
```bash
git clone git@github.com:username/repository.git
```
