# Using SSH and Github on the Remote ieng6 Machine
![](https://kinsta.com/wp-content/uploads/2022/01/generate-ssh-key.jpg)
<br/>

## What we will go over:
1. Streamlining ssh Configuration
2. Setting up Github Access on ieng6
3. Copying Entire Directories
<br/>

### 1. Streamlining ssh Configuration
Since by now we have already established our own public and private ssh key on our local machine and shared the public key with the remote ieng6 machine, we can further streamline the ssh remote connection process.
* We do this by first creating a new file called `config` (no file extention) in the `.ssh` directory on our local machine
    * You can create the file by locating and openning the `.ssh` directory in VS code on your local machine.
    * Then once you've created the config file, add the following text:
        ```
        Host ieng6
            HostName ieng6.ucsd.edu
            User cs15lsp22zzz (use your username)
        ```
        The `ieng6` on the first line is an alias that can be changed to whatever you prefer. This is what you will be typing instead of the super long email address to `ssh` into the remote machine from now on.
        ![](..\images\labReport3\config.jpg)
* Once everything is set up properly, you can just type `ssh <whatever alias you chose>` to connect to the remote machine
![](..\images\labReport3\configSsh.jpg)
* You can also use the alias in `scp` to reference the remote machine
![](..\images\labReport3\configScp.jpg)

### 2. Setting up Github on the Remote ieng6 Machine
Now that we can access the remote machine much faster, we can begin to look at streamlining our Github commands. Because Github recently stopped supporting password authentication for pushing to a repository, we have to set up a `ssh` key on the remote machine for Github.
* To set up a `ssh` key for Github, first follow this tutorial: [Checking for existing keys](https://docs.github.com/en/articles/checking-for-existing-ssh-keys)
* Then follow this tutorial: [Generating a new key](https://docs.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
    * Your private and public keys should both be stored in the `.ssh` directory on the ieng6 machine.
    ![](..\images\labReport3\githubKeys.jpg)
* Finally, bring everything together with this tutorial: [Adding a ssh key to Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
![](..\images\labReport3\githubRemoteKey.jpg)

* If everything runs correctly, then you will be able to push commits from the remote machine without needing to type in a username and password every time. 
![](..\images\labReport3\githubPush.jpg)
    * Link to commit: [https://github.com/EdwardNew/markdown-parser/commit/48a91d6ea2949094ce4610580e505b22004cfa4b](https://github.com/EdwardNew/markdown-parser/commit/48a91d6ea2949094ce4610580e505b22004cfa4b)
    ![](..\images\labReport3\githubCommit.jpg)

* If you did everything correctly and it is still not working, you may have to type this command:
    ```
    git remote set-url origin git@github.com:<Username>/<Project>.git
    ```
    where the username is your Github username and the project is the name of your repository.
    I personally ran into issues and [this](https://stackoverflow.com/questions/14762034/push-to-github-without-a-password-using-ssh-key) helped me solve them.

### 3. Copying Entire Directories
Up until this point, we have been copying files one by one or copying directories that are empty. We can copy entire directories and their subdirectories by simply adding a `-r` argument after the `scp` command to copy the directory recursively.
```
$ scp -r . cs15lsp22@ieng6.ucsd.edu:~/markdown-parse
```
* The `.` represents the source directory that is being copied
* The `cs15lsp22@ieng6.ucsd.edu` can now be replaced with the alias we have chosen in our config file
* The file path after the `:` specifies where we want our directory copied to on the remote machine
    * If the directory specified does not exist, a new one will be created with the given name
* You can also use `*.java` or `*.<insert file extension>` before the source directory to specify only certain types of files be copied over

Here is an example of how this can be used:
![](..\images\labReport3\scp1.jpg)
![](..\images\labReport3\scp2.jpg)
![](..\images\labReport3\scpCompile.jpg)

We can further streamline this process by trying to condense the commands for copying to, and testing on, the remote machine onto one line:
![](..\images\labReport3\scp1Line1.jpg)
![](..\images\labReport3\scp1Line2.jpg)

* Some common errors that occured were that the version of java run when using a `ssh` one line command is different from the versions we are used to. To ensure smooth compiling and running do the following:
    * remove `.class` files from your local directory before copying
    * remove `.class` files from the remote directory if you've already copied them over from the local directory
    * check that these two import statements are in the Test file:
        ```
        import java.nio.file.Files;
        import java.nio.file.Path;
        ```
    * replace `javac` with `/software/CSE/oracle-java-17/jdk-17.0.1/bin/javac` and `java` with `/software/CSE/oracle-java-17/jdk-17.0.1/bin/java` to specify which exact version of java to use

## Congrats!
By now you should have a much more efficient workflow that has minimal tedious repetitive commands. Now you can put all that extra time into actually writing your programs!