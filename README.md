## Overview
This process involves generating an RSA key pair that will be used to securely access the student environment. The public key will be stored on the student environment, with the private key kept on our local machine.

We also create an SSH configuration, which: 1. specifies that our private key should be used when connecting to the student environment, and 2. defines a customizable alias for the host name.

## Instructions
### Generate an SSH key

1. Open a terminal.
2. Run the following command:
```bash
ssh-keygen
```
##### If you're on Mac
3. At the prompt, enter the text below, substituting your Mac username in for `username`:
```bash
/Users/username/.ssh/cs_key
```
4. Press `Enter` at the remaining prompts.

##### If you're on Linux / Bash on Ubuntu on Windows
3. At the prompt, enter the text below, substituting your Mac username in for `username`:
```bash
/home/username/.ssh/cs_key
```
4. Press `Enter` at the remaining prompts.

##### If you're using Git Bash
3. At the prompt, enter the text below, substituting your Mac username in for `username`:
```bash
/c/Users/username/.ssh/cs_key
```
4. Press `Enter` at the remaining prompts.

---
### Set up SSH configuration file
1. Create or edit the SSH configuration file at `~/.ssh/config`. Add an entry containing the following:
```bash
Host cs
    HostName linux.student.cs.uwaterloo.ca
    User watiam_id
    IdentityFile ~/.ssh/cs_key
```
**Notes**:
* Replace `watiam_id` with your own ID.
* Feel free to change the value for `Host` – this value is what you will type when using the `ssh` command in the future.


### Copy the newly generated key to the server
1. Print the contents of your public key file with:
```bash
cat ~/.ssh/cs_key.pub
```
2. Copy the output to the clipboard.
3. `ssh` into the student environment with:
```bash
ssh cs
```
(replacing `cs` with your `Host` value, if different)

4. Create or edit `~/.ssh/authorized_keys`:
    * You will need to create the `.ssh` directory if it does not exist.
5. Paste the content from your clipboard **on its own single line** in the file. If the file is not empty, add a line at the end of the file. It should look something like this:
```
ssh-rsa
AAAAB3NzaC1yc2EAAAADAQABAAABAQDWSwzGvsYHCAZ2g6xccbGBdNb6wBbghd7kspx6
eTPt4RSlLPEewBg3qogyj3I+DSa2M+Mql8xG4A6TLj7mOeIrS6BDcX5NEi3mStN5Bt+j
j1SqRJYceD93a7RjPaaaaakjakdshfklhasldkhflkasdjhfaksjldhfhXjIm7RIFjiv
q56TpK8HXd/YXD29IY4o4MPr6rXJcMKws5fnl3kywYRwv7Hg9mPKdHnKm9En2PXtq7BX
VlNz+lQt1cQ9GpKHiPt69GlzervXGSFt54eaddTrEbzzesoZ4OtDbnwWEh3Pp95FvZFd
ejLbIakpUTJnPCWU7EAGCV4Me1thDZQ5 alex@Alexs-MacBook-Pro.local
```
  * The content may be split over 2 lines by default. A good way to check that it is on one line is with `wc`, or by displaying line numbers in `vi` by typing `:set number` while in Normal mode.
6. Save the file.

---

You should now be able to `ssh` into the student environment without being asked for a password.
