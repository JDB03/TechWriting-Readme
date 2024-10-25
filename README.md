# Team Mountaineers Programming Setup Process

## Important Notes
$ means run in a terminal
cd is change directory
ls lists out files and folders in the current directory


## Setting Up Ubuntu (Virtual Machine)

## Setting Up Ubuntu (Dual Boot)

## Setting Up GitHub
1. Open a new terminal and create and SSH Key by running the command `$ ssh-keygen`. Keep the default file name, and add a password if you want to.

2. Go to [https://github.com/settings/keys](https://github.com/settings/keys) and select the 'New SSH Key' button.

3. Title this key whatever you want but make sure the 'Key type' is 'Authentication Key'.

4. Copy and paste the output of `$ cat ~/.ssh/id_rsa.pub` into the 'Key' field and select 'Add SSH key'

5. Run the command `$ git config --global user.email "\<your email>" to set the email associated with your commits

6. Run the command `$ git config --global user.name "\<your username>" to set the username associated with your commits

## Setting Up The URC Repo

1. Before setting up the URC Repo make sure you are in the correct place. To do this, open a new terminal and ensure that the text printed automatically looks similar to `username@computer:~$`. The current directory should be `~` and not anything else. If your terminal does not look like this, run the command `$ cd` without arguments to move back to your home directory.

2. Run the command `$ git clone git@github.com:wvu-urc/workspace-newrobot2025.git workspace-newrobot2025`. This command will clone the current repo into a folder named `$ workspace-newrobot2025` in your home directory.

3. Run the command `$ cd workspace-newrobot2025` to move the current terminal into the newly downloaded repo. The text printed automatically should look similar to `username@computer:~/workspace-newrobot2025$`.

4. Run the command `$ ./setup/install_humble.bash` to download ROS2 Humble and the other packages we use. This will take a while to install, 10-30 minutes in total depending on internet connection

5. Make sure you are still in the `$ workspace-newrobot2025` directory (`username@computer:~/workspace-newrobot2025$`). If you aren't, run the command `$ cd ~/workspace-newrobot2025`. After ensuring this, run the command `$ source ~/.bashrc` to reload environment variables and give the current terminal access to ROS2.

6. Run the command `vcs import src < repos.yaml` to import all of the additional packages into the repo. Usually this will output text indicating the download of several packages, but two known failures can occur (See [Troubleshooting](#Troubleshooting) for more information)

7. Install Additional Dependencies by running the command `$ rosdep install --from-paths src --ignore-src -r -y`. This will install all the specific dependencies that are in packages you just downloaded.

8. Compile the workspace by running `$ colcon build`. See [Troubleshooting](#Troubleshooting) if you encounter errors or crashes.

9. After running the above commands, you should have a directory structure that follows something similar to this:
   ```
    /workspace-newrobot
       /build
       /install
       /log
       /scripts
       /setup
       /src
         /autonomy
           /autonomy_2025
         /infrastructural_packages
           /robot_interfaces
         /subfolder3
           /additional_pkg1
           /additional_pkg2
         /...
           /...
   ```

## Making Your Own Package

## Running Code

# Troubleshooting
