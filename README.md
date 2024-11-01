![image](https://github.com/user-attachments/assets/abeb69cd-fd83-4995-95dd-37435209c01f)# Team Mountaineers Programming Setup Process
This ReadMe Document is Specifically for the 2024-2025 Competition Year

## Important Notes
- `$` means to run this command in a terminal
- `$ ls` will list out files and folders in the current directory
- `$ cd` stands for change directory
   - `$ cd /<directory>` will change to a specific directory at a lower level than this one (Like opening a folder in file explorer)
   - `$ cd ..` will move you back up one level
- When Copying or Pasting in the Ubuntu Terminal, `Ctrl` + `C` and `Ctrl` + `V` do not work. You must use `Ctrl` + `Shift` + `C` and `Ctrl` + `Shift` + `V`

## Using the Ubuntu Terminal
- sudo password
- ls
- cd
- copy and paste
- directories

## Setting Up Ubuntu (Virtual Machine)

1. Download the URC-2025.ova from the Google Drive [Link](https://drive.google.com/drive/u/0/folders/1vqS1py4Nn8kZ3vGHXefXxz-EPyCs_CXJ)

2. Download the VirtualBox host associated with the operating system you are currently using [Download Page](https://www.virtualbox.org/wiki/Downloads) 
   - When installing, you may encounter a Python Binding Error, this is fine and you can ignore it.

3. Open VirtualBox and select 'Import Appliance' from the File Dropdown in the top left corner

4. Import the .ova file that you downloaded from the Google Drive

5. Click Next and Tweak the Appliance Settings as you see fit (the defaults should work for most people)

6. Wait while it imports

7. Run the Virtual Machine by double clicking the new entry in the list off to the left, the password is the same as the username (If you have trouble getting it functional, see [Troubleshooting](#VirtualBox)

## Using the Ubuntu Terminal

1. 

## Setting Up GitHub

1. Open a new terminal and create and SSH Key by running the command `$ ssh-keygen`. Keep the default file path by pressing enter, and add a password if you want to (not strictly necessary).

2. Go to [https://github.com/settings/keys](https://github.com/settings/keys) and select the 'New SSH Key' button.

3. Title this key whatever you want but make sure the 'Key type' is 'Authentication Key'.

4. Copy and paste the output of `$ cat ~/.ssh/id_rsa.pub` into the 'Key' field and select 'Add SSH key'

5. Run the command `$ git config --global user.email "\<your email>"` to set the email associated with your commits

6. To set the username associated with your commits, run the command `$ git config --global user.name "\<your username>"`

## Setting Up The URC Repo

1. Before setting up the URC Repo make sure you are in the correct place. To do this, open a new terminal and ensure that the text printed automatically looks similar to `username@computer:~$`. The current directory should be `~` and not anything else. If your terminal does not look like this, run the command `$ cd` without arguments to move back to your home directory.

2. Run the command `$ git clone git@github.com:wvu-urc/workspace-newrobot2025.git workspace-newrobot2025`. This command will clone the current repo into a folder named `$ workspace-newrobot2025` in your home directory.

3. Run the command `$ cd workspace-newrobot2025` to move the current terminal into the newly downloaded repo. The text printed automatically should look similar to `username@computer:~/workspace-newrobot2025$`.

4. Run the command `$ ./setup/install_humble.bash` to download ROS2 Humble and the other packages we use. This will take a while to install, 10-30 minutes in total depending on internet connection
- There are certain points when you will be prompted with the option `(Y/n)` or `(y/n)`. In both cases, type `y` into the terminal and hit enter to accept

5. Make sure you are still in the `$ workspace-newrobot2025` directory (`username@computer:~/workspace-newrobot2025$`). If you aren't, run the command `$ cd ~/workspace-newrobot2025`. After ensuring this, run the command `$ source ~/.bashrc` to reload environment variables and give the current terminal access to ROS2.

6. Run the command `vcs import src < repos.yaml` to import all of the additional packages into the repo. Usually this will output text indicating the download of several packages, but two known failures can occur (See [Troubleshooting](#Troubleshooting) for more information)

7. Install Additional Dependencies by running the command `$ rosdep install --from-paths src --ignore-src -r -y`. This will install all the specific dependencies that are in packages you just downloaded.

8. Compile the workspace by running `$ colcon build`. See [Troubleshooting](#Troubleshooting) if you encounter errors or crashes.

9. After running the above commands, you should have a directory structure that follows something similar to this:
   ```
    /workspace-newrobot2025
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
   This can be checked by opening the Ubuntu File explorer and checking to see the contents of the `workspace-newrobot2025` folder

## Making Your Own ROS2 Package

1. Go to [https://github.com/orgs/wvu-urc/repositories](https://github.com/orgs/wvu-urc/repositories) and select the New Repository Button.

2. Give this repository a descriptive name and leave it Private. Select Add a README file and choose MIT License from the dropdown menu. Then Create the repository

3. Open `workspace-newrobot2025` in the code editor of your choice and open the `repos.yaml` file in the main level of the workspace.

4. Add your new repo in with the following format:
   ```
   <category>/<package_name>:
     type: git
     url: <ssh_clone_code>
     version: <branch>
   ```
   - `\<category>` is the general category your package falls into (i.e. autonomy, hardware_interfacing, user_interfacing)
   - `\<package_name>` is the name you gave your repository
   - `\<ssh_clone_code>` is the link copied from the code button on your repositories page (in the format of `git@github.com:wvu-urc/<package_name>.git`)
   - `\<branch>` is the specific branch of your repo you want included
  
5. In your code editor, open the `.gitignore` file in the main level of the workspace and add `src/<category>/<package_name>` to the list of ignored folders
  
6. Run the command `vcs import src < repos.yaml` to import all of the additional packages into the repo. Usually this will output text indicating the download of several packages, but two known failures can occur (See [Troubleshooting](#Troubleshooting) for more information)

7. Navigate in a terminal to the category folder of new repo you just downloaded. It should be located at `~/workspace-newrobot/src/<category>

8. Run the command `$ mv ./<package_name> ./<package_name>2 .` to rename the package folder temporarily. This command doesn't give any outputs but you can check it worked by running `$ ls`. This output should contain `<package_name>2` instead of `<package_name>`
   
9. Run the command `$ ros2 pkg create --build-type ament_python <package_name>` to make the ROS2 package

10. Run the command `$ cp -a /<package_name>2/. /<package_name>/; rm -rf /<package_name>2` to merge the files of the two folders together.  This command doesn't give any outputs but you can check it worked by running `$ ls`. This output should now contain `<package_name>` not `<package_name>2`

11. Run `$ cd ~/workspace-newrobot2025` to get back to the top level of the workspace. Once there, compile the workspace by running `$ colcon build`. See [Troubleshooting](#Troubleshooting) if you encounter errors or crashes. 

## Running Code

1. Move to the top level of the workspace by running the command `cd ~/workspace-newrobot2025`

2. Make sure your code is up to date by running `vcs pull src`

3. Compile the workspace by running `$ colcon build`. See [Troubleshooting](#Troubleshooting) if you encounter errors or crashes.

4. Allow files to be run by your terminal by running `$ source install/setup.bash`

5. Run code in one of the following ways:
   - `ros2 run <package_name> <node_name>`
   - `ros2 launch <packate_name> <launch_file_name>`
   - `ros2 launch launches/<launch_file_name>`
   If you run into errors or crashes, See [Troubleshooting](#Troubleshooting).

# Troubleshooting

## VirtualBox
- If you get a black screen on startup try reimporting the OVA
- If you aren't able to see anything on a computer with a 4K display, select view in the top menu bar and manually set your resolution to `1920 x 1080` or `1920 x 1200` and set the scale factor to `200%`
- If you are using Windows and have WSL2 installed you may encounter a slow VM or one that doesn't run at all. To solve this problem, search `Turn Windows Features on or off` in the windows search bar and uncheck `Virtual Machine Platform`. This will disable WSL2 until you re-enable it, at which point your VirtualBox problems may start happening again.

## VCS Tool isn't working
- `Input data is not valid format: 'NoneType' object is not subscriptable`
   - This error is cause by the repos.yaml file being empty. Check with one of the Programming coordinators to see if this should be the case
- Most of the Imports are failing
   - WVU has anti-spam protection set up in place and that causes issues when downloading our repositories at once. Try waiting a few minutes and running the command again. If that doesn't work, try using another internet source like a mobile hotspot.

 ## Errors when Running `colcon build`
- Most errors are related to specific packages so see if a particular one is mentioned
   - If a python stack trace is shown the code in that package is messed up
- `The current CMakeCache.txt <directory> is different than the directory <directory> where CMakeCache.txt was created. This may result in binaries being created in the wrong place.`
   - Run `$ rm -rf ./log ./install ./build` to clear the workspace, then try building again
- `The source directory <directory> does not exist`
   - Run `$ rm -rf ./log ./install ./build` to clear the workspace, then try building again
- My computer / VM keeps crashing when building the code
   - `colcon build` uses a lot of computing resources and can sometimes starve out other important processes. If this keeps happening, try running `$ colcon build --executor sequential` instead. This will reduce the number of packages it tries to build at once from 4 to 1
