# Fixing Obsidian Git Password Prompts on Linux

When Obsidian (or a background sync script) triggers a Git action, it cannot access your terminal's active `ssh-agent`. If your default SSH key is password-protected, the system will repeatedly throw a graphical popup window asking you to unlock the protected file.

The permanent, hassle-free fix is to route that specific repository to a dedicated, unencrypted (passwordless) SSH key.

---

### 1. Generate a Passwordless Key
Create an SSH key specifically for your Obsidian vault. When prompted for a passphrase, **press Enter twice** to leave it completely blank:
```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_obsidian_git -N ""
```

### 2. Add the New Public Key to GitHub
Print the contents of your new public key file:
```bash
cat ~/.ssh/id_obsidian_git.pub
```
Copy the entire output string and add it to your profile:
* **GitHub** &rarr; **Settings** &rarr; **SSH and GPG keys** &rarr; **New SSH Key**

### 3. Update the Vault's Internal Git Config
Navigate into your local vault repository and open its hidden local configuration file:
```bash
cd /path/to/your/obsidian/vault
nano .git/config
```
Under the `[core]` section, add or modify the `sshCommand` line to explicitly target your new passwordless key file:
```ini
[core]
    sshCommand = "ssh -i ~/.ssh/id_obsidian_git"
```
*Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).*

### 4. Ensure Correct File Permissions
If OpenSSH complains about permissions being too open, lock down the `.ssh` assets securely:
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_obsidian_git
chmod 644 ~/.ssh/id_obsidian_git.pub
```
