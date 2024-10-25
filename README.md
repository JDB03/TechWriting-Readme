# Team Mountaineers Programming Setup Process

## Setting Up Ubuntu (Virtual Machine)

## Setting Up Ubuntu (Dual Boot)

## Setting Up GitHub

## Setting Up The URC Repo

1. Before setting up the URC Repo make sure you are in the correct place. To do this, open a new terminal and ensure that the text printed automatically looks similar to `username@computer:~$`. The current directory should be `~` and not anything else.

2. Run the command `git clone git@github.com:wvu-urc/workspace-newrobot2025.git workspace-newrobot2025`. This command will clone the current repo into a folder named `workspace-newrobot2025` in your home directory.

3. Run the command `cd workspace-newrobot2025` to move the current terminal into the newly downloaded repo. The text printed automatically should look similar to `username@computer:~/workspace-newrobot2025$`.

4. Run the command `vcs import src < repos.yaml` to import all of the additional packages into the repo. Usually this will output text indicating the download of several packages, but two known failures can occur (See [Troubleshooting](##Troubleshooting))

### Make Sure you are in the home directory

### mkdir workspace-newrobot2025

### cd workspace-newrobot2025

### git pull ssh key

### vcs import

## Making Your Own Package

## Running Code

## Troubleshooting
