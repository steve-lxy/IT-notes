## su

The **`su`** command in Linux lets you switch to another user's account or execute commands as a different user. 

```bash
su [options] [username]
```

The **`[username]`** represents the user account you want to switch to or execute commands as. If not specified, the default is the [root](https://phoenixnap.com/glossary/what-is-root-access) user.

 **`[options]`** are not mandatory, but when used, they modify the **`su`** command. 

| **`-`**, **`-l`**, **`--login`**    | Makes the shell a login shell, which means it reads the user's login profile and initializes the environment as if the user had logged in directly. |
| ----------------------------------- | ------------------------------------------------------------ |
| **`-c`**, **`--command [command]`** | Passes a single command to the shell after switching users.  |

### `su` vs. `su -`

When you use **`su`**, the system switches to the specified user's account but **keeps the current environment**, including the current working directory, shell variables, and other settings. It doesn't fully simulate a login session as the specified user.

On the other hand,**` su -`** or **`su -l`** or **`su --login`** simulates a full login session for the specified user. It resets the environment to that of the target user, including the home directory, shell, and environment variables.

## sudo

The sudo command grants limited-time access to root functionality. This command allows you to execute administrative commands temporarily and then return to regular user permissions. This is especially useful for tasks that require elevated privileges but don't need constant root access. Users gain `sudo` access by being added to the sudo group.

**`su`** doesn't require users to be added to specific groups. However, the target user's password is required to switch accounts.

Additionally, **`su`** can mimic **`sudo`** functionality using the **`-c`** option to execute a single command as another user without starting an interactive session.

#### Add user to sudo group

With root privilege, add users to sudoers:

For CentOS:

```bash
usermod -aG wheel [username]
```

For Debian:

```bash
usermod -aG sudo [username]
```

You may need to reboot the Linux to make it effect.

You can directly edit config file using `visudo` command.

#### Installation

If sudo is not installed, switch to root to install it:

```bash
su -
apt-get install sudo -y
```

#### If sudo command can not be executed, try this:

```bash
pkexec su
```

