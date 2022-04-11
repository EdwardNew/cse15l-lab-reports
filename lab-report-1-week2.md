# Connecting to the ieng6 Remote Machine

![](images\labReport1\sshImg.png)

## What we will go over:
1. Installing VS Code
2. Remote Connecting
3. Trying Some Commands
4. Moving Files with `scp`
5. Setting an SSH Key
6. Optimizing Remote Running

### 1. Installing VS Code (For Windows)
* Go to [https://code.visualstudio.com](https://code.visualstudio.com/)
![](images\labReport1\downloadVSCode.jpg)

* Click on the Download button

* Open the program once it is installed!
![](images\labReport1\VSCode.jpg)

<br/>

### 2. Remotely Connecting (Via SSH)
* Install both OpenSSH Client and OpenSSH Server (Only for Windows)
    * Settings>Apps>Apps & Features>Optional Features>Add a Feature
    ![](images\labReport1\Openssh.jpg)

* Look up your account [here](https://sdacs.ucsd.edu/~icc/index.php)
    * Your username should be something like:  cs15lsp22~~~@ieng6.ucsd.edu
    <br/>
    (The ~~~ should be unique to your account)


* Open a terminal on your local client machine
    * Type in `$ ssh cs15lsp22~~~@ieng6.ucsd.edu`
    * If it's the first time logging into the server, you might get a message about RSA key fingerprints, just enter `yes` to continue
    * Type in your password (**IT IS NORMAL TO NOT SEE YOUR PASSWORD BEING ENTERED, CONTINUE TO TYPE YOUR PASSWORD NORMALLY**)
    * You should now be logged in
    ![](images\labReport1\SshLoggedIn.jpg)

<br/>

### 3. Trying Some Commands
* Try some commands in the terminal!
    * `cd` Change directory
    * `ls` List files in current directory
    * `cp` Copy a file to another location
    * `touch` Creates an empty file
    * `cat` Creates an empty file, allows you to open existing files, allows you to add to existing files
    * `man` Gives details about a specific command
    * Look [here](http://mally.stanford.edu/~sr/computing/basic-unix.html) for more commands to try

![](images\labReport1\UnixCommands.jpg)

<br/>

### 4. Moving Files with `scp`
* Create or Choose an existing file in your current local/client directory
* Type `$ scp <filename> <remote directory file path>`
    * Example: `$ scp WhereAmI.java cs15lsp22atk@ieng6.ucsd.edu:~/`
        * Moves the WhereAmI java file to the home directory of the remote machine
* You will have to enter your password everytime you `scp` to authenticate yourself to the remote machine

![](images\labReport1\SCP.jpg)

<br/>

![](images\labReport1\SCPRemote.jpg)

<br/>

### 5. Setting an SSH Key
* To avoid having to enter your password everytime you `ssh` or `scp`, you can create a SSH Key that authenticates your machine automatically
* In your local/client terminal, type `$ ssh-keygen`
     * When prompted for what file to store the key in, enter `/Users/<user-name>/.ssh/id_rsa`
     * When prompted for a passphrase, just hit Enter, leaving it blank
        * Repeat this when asked to confirm passphrase
    * You should get a grid of symbols followed followed by a `SHA-256`
    * This means your keys have been created
* Now you need to copy your public key to the .ssh directory on the remote machine
    * Log in to the remote machine and create a new directory called .ssh using the `$ mkdir .ssh` command
    * Now go back to your local/client directory and scp the public key to the new directory you just created using:
    <br/>

    `scp /Users/<user-name>/.ssh/id_rsa.pub cs15lsp22~~~@ieng6.ucsd.edu:~/.ssh/authorized_keys`

    * If this does not work, makee sure you have:
        * entered the username of your local/client machine correctly
        * entered the username of your remote machine correctly
    * If it still does not work, try to create a new file named authorized_keys in the .ssh directory using the `$ touch authorized_keys` command before trying the `scp``` command again

* When everything works, try logging into the remote machine. You should automatically be authenticated, no password needed.

![](images\labReport1\sshkey.jpg)

### 6. Optimizing Remote Running
* To make life even easier on us, we can reduce the amount of keystrokes needed to `scp` a file from our local/client directory to the remote directory
* We do this by taking advantage of the fact that you can have multiple commands run on the same line
* If you wanted to copy a file from your local machine to the remote machine, compile and run it on the remote machine, you can `scp` first, separate that command and the next with a `;`, then `ssh` into the remote machine again and compile and run the file
    * Example: ![](images\labReport1\onelinecommand.jpg)
    * Individual commands can be written on one line in the terminal as long as they are separated by a `;`
    * The `scp` command only signs into the remote machine to copy the file, then logs out automatically
        * This is why we need to `ssh` into the remote machine again to compile and run the file we copied
    * The `ssh` command logs you into the remote machine but if followed by another command, it will log in, run the command and automatically log out again
        * Since we want to keep this behavior but want to run more than 1 command (compile *and* run), we can enclose our commands in `" "` so the `ssh` run everything contained before it automatically logs out again
            * Thus we have `"javac WhereAmI.java; java WhereAmI"`

<br/>

## Congrats!
If you've made it this far, you're all set up to start working on the remote machine ieng6!