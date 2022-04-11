# Connecting to the ieng6 Remote Machine

![](images\labReport1\sshImg.png)

## What we will go over:
1. Installing VS Code
2. Remote Connecting
3. Trying Some Commands
4. Moving Files with ```scp```
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
    * Your username should be something like:  cs15lsp22***@ieng6.ucsd.edu
    <br/>
    (The *** should be unique to your account)


* Open a terminal on your local client machine
    * Type in ```$ ssh cs15lsp22***@ieng6.ucsd.edu```
    * If it's the first time logging into the server, you might get a message about RSA key fingerprints, just enter ```yes``` to continue
    * Type in your password (**IT IS NORMAL TO NOT SEE YOUR PASSWORD BEING ENTERED, CONTINUE TO TYPE YOUR PASSWORD NORMALLY**)
    * You should now be logged in
    ![](images\labReport1\SshLoggedIn.jpg)

<br/>

### 3. Trying Some Commands
* Try some commands in the terminal!
    * ```cd``` Change directory
    * ```ls``` List files in current directory
    * ```cp``` Copy a file to another location
    * ```touch``` Creates an empty file
    * ```cat``` Creates an empty file, allows you to open existing files, allows you to add to existing files
    * ```man``` Gives details about a specific command
    * Look [here](http://mally.stanford.edu/~sr/computing/basic-unix.html) for more commands to try

![](images\labReport1\UnixCommands.jpg)

<br/>

### 4. Moving Files with ```scp```
* 