---
title: "1.2 Setting Up Git, GitHub, and SSH"
date: 2025-07-20
---

<!-- # 1.2 Setting Up Git, GitHub, and SSH -->

## Install Git

### *Mac*
- Install homebrew and follow the terminal instructions

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Install git

```bash
brew install git
```

### *Windows*

- Install [Git for Windows](https://gitforwindows.org/), which provides Git Bash (terminal emulator for running Git commands)
  
- Or- install using Windows Powershell
```bash
winget install --id Git.Git -e --source winget
```

- Note: if the above command didn't work, you may need to install [winget](https://chxtio.github.io/ocr_jekyll/) first

```bash
$progressPreference = 'silentlyContinue'
Write-Host "Installing WinGet PowerShell module from PSGallery..."
Install-PackageProvider -Name NuGet -Force | Out-Null
Install-Module -Name Microsoft.WinGet.Client -Force -Repository PSGallery | Out-Null
Write-Host "Using Repair-WinGetPackageManager cmdlet to bootstrap WinGet..."
Repair-WinGetPackageManager
Write-Host "Done."
```

- You can also install Linux for Windows via [WSL (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
  - Once setup, Git can be installed using the Linux package manager 

### *Ubuntu*

- Install Git

```bash
sudo apt install git
```

## Configure Git
- Configure Git, replacing `"Your name"` and `"your.email@example.com"` with your info (including the quotes) to link your local Git profile with GitHub

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

- Verify configuration
  
```bash
git config --get user.name
git config --get user.email
  ```

## Set up SSH
- Create a new SSH key using your GitHub email as a label

**Note: Press enter to skip through the 3 prompts that follow**

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

- Copy the public key to your GitHub account (See [example](https://github.com/Training-Dummy/howtoforge_git_ubuntu/blob/master/README.md#creating-an-ssh-key))

```bash
cat ~/.ssh/id_ed25519.pub
```

- In GitHub, navigate to [**Settings -> SSH and GPG keys -> New SSH Key**](https://github.com/settings/ssh/new) and paste it there ([example](https://camo.githubusercontent.com/6d19b54f3f16f98804e3b33804d6eb2fa82fb2e796dbce825f8cba2f4b3f74a3/68747470733a2f2f692e696d6775722e636f6d2f676466624a4b6a2e706e67))


- Confirm that your SSH key is connected to your GitHub account

```bash
ssh -T git@github.com
```

- if successful, you should see:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```
