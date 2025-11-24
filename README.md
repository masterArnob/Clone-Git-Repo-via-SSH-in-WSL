# Clone Git Repo via SSH in WSL (Windows Subsystem for Linux)

Step-by-step guide to set up SSH keys in WSL and clone Git repositories without password.

### Step 1: Open WSL
```bash
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

### Step 4: Check the public key
```bash
cat ~/.ssh/id_ed25519.pub
```


### Step 5: Generate Key
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Step 6: Copy the public key
```bash
cat ~/.ssh/id_ed25519.pub | clip.exe
```

### step 7: Put key to github
```bash
GitHub → Settings → SSH and GPG keys → New SSH key → paste
```



### Step 8: Run this
```bash
echo -e "\n# ==== WSL SSH Agent Auto Start ====\nif [ -z \"\$SSH_AUTH_SOCK\" ]; then\n    eval \"\$(ssh-agent -s)\" > /dev/null\n    ssh-add ~/.ssh/id_ed25519 2>/dev/null\nfi" >> ~/.bashrc && source ~/.bashrc && echo "Done! SSH agent will start automatically now."
```



### Step 9: SSH connection test
```bash
ssh -T git@github.com
```

### Step 10: Change directory
```bash
cd /d E:\Laravel\Laravel_Projects
```

### Step 11: Clone Repository
```bash
git clone git@github.com:username/repository.git
```


### Cloning github repository
```groovy
pipeline{
    agent any
    
    environment{
        SSH_CREDENTIALS = 'my-ssh-private-key'
        REPOSITORY_URL = 'git@github.com:Faizanabid36/mon-cherri.git'
    }
    
    stages{
        stage('cloning-repo'){
            steps{
                echo "start cloning..."
            
                sshagent(credentials: ["${SSH_CREDENTIALS}"]){
                    sh 'git clone ${REPOSITORY_URL}'
                 }
                
                echo "clonnig finish..."
            }
        }
    }
}
```

### Cloning repository of specific branch
```
pipeline{
    agent any
    
    environment{
        SSH_CREDENTIALS = 'my-ssh-private-key'
        REPOSITORY_URL = 'https://github.com/masterArnob/testing.git'
        BRANCH_NAME = 'masterArnob-patch-1'
        APP_NAME = 'testing'
    }
    
    stages{
        stage('cloning-repo'){
            steps{
                echo "start cloning..."
            
                sshagent(credentials: ["${SSH_CREDENTIALS}"]){
                    sh 'rm -rf ${APP_NAME}'
                    sh 'git clone --branch ${BRANCH_NAME} --single-branch ${REPOSITORY_URL} ${APP_NAME}'
                 }
                
                echo "clonnig finish..."
            }
        }
    }
}
```
