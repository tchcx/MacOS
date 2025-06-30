# MacOS
Collected Notes From Setting Up My New Mac to Not be a Filesystem and Configuraion Cesspool




## Homebrew
- If you use multiple user accounts (like my "personal" and "instructor" accounts...
- Install homebrew
- Make a third **homebrew** user (doesn't need to be an admin)

<img width="467" alt="image" src="https://github.com/user-attachments/assets/404a9e1e-3abe-4cbf-a89f-88e387d2d7fb" />

- Change ownership for brew
```
sudo chown -R homebrew /opt/homebrew /opt/homebrew/Cellar \
/opt/homebrew/Frameworks /opt/homebrew/bin /opt/homebrew/etc \
/opt/homebrew/etc/bash_completion.d /opt/homebrew/include \
/opt/homebrew/lib /opt/homebrew/opt /opt/homebrew/sbin \
/opt/homebrew/share /opt/homebrew/share/doc /opt/homebrew/share/man \
/opt/homebrew/share/man/man1 /opt/homebrew/share/man/man3 \
/opt/homebrew/share/zsh /opt/homebrew/share/zsh/site-functions \
/opt/homebrew/var/homebrew/linked /opt/homebrew/var/homebrew/lock
```

- Change permissions (or just to be safe...)
```
sudo chmod u+w /opt/homebrew /opt/homebrew/Cellar /opt/homebrew/Frameworks \
/opt/homebrew/bin /opt/homebrew/etc /opt/homebrew/etc/bash_completion.d \
/opt/homebrew/include /opt/homebrew/lib /opt/homebrew/opt /opt/homebrew/sbin \
/opt/homebrew/share /opt/homebrew/share/doc /opt/homebrew/share/man \
/opt/homebrew/share/man/man1 /opt/homebrew/share/man/man3 /opt/homebrew/share/zsh \
/opt/homebrew/share/zsh/site-functions /opt/homebrew/var/homebrew/linked \
/opt/homebrew/var/homebrew/locks
```

- Add this to all users' .zshrc files:
```
alias brew="sudo -Hu homebrew brew"
```

- Before updating **sudoers**
![image](https://github.com/user-attachments/assets/2955e909-5392-457e-8bd2-ba8c1c47721e)

- Update **sudoers** so non-admin users can still use homebrew (the user) via sudo
```
# loki can run all commands as homebrew (user)
# we could lock this down more if needed
# but homebrew isn't an admin user anyway
loki            ALL=(homebrew) ALL

# To allow Powershell to be installed
homebrew        ALL= (ALL) NOPASSWD:SETENV: /usr/sbin/installer
```

- After updating **sudoers**
<img width="859" alt="image" src="https://github.com/user-attachments/assets/0495801d-9fa4-4244-9165-1e996f25b177" />

- Other users can use it, yay! Make sure brew is in everyone's $PATH
<img width="697" alt="image" src="https://github.com/user-attachments/assets/396deab5-f329-486d-856c-f1507f0d194b" />

- Hide user account from login screen (inconsistently, in my experiennce):
```
sudo dscl . create /Users/homebrew IsHidden 1
```
