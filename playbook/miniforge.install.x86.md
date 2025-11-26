# Miniforge Ansible Installer

This set of scripts installs Miniforge to a remote Linux server without requiring sudo privileges. It uploads a locally downloaded installer to the remote server and executes it.

## Prerequisites

1.  **Download Miniforge Locally**: You must have the installer script on your machine (the one running Ansible).
    
    ```
    wget [https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh)
    chmod +x Miniforge3-Linux-x86_64.sh
      
    
    ```
    
2.  **Update Inventory**: Edit 
    ```
    inventory.yml
    ```
    :
    
      16.   Update 
          ```
          ansible_host
          ```
           and 
          ```
          ansible_user
          ```
          .
          
      26.   Ensure the following variables are set correctly:
          ```
          package_base_dir
          ```
          points to the base directory containing your packages (e.g., "~/packages"),
          ```
          installer_relative_path
          ```
          is the subdirectory path under package_base_dir (can be empty if installer is directly in package_base_dir), and
          ```
          installer_filename
          ```
          is the name of your installer file (e.g., "Miniforge3-Linux-x86_64.sh"). The full path will be constructed as package_base_dir + installer_relative_path + installer_filename.
          
      32.   Ensure 
          ```
          miniforge_install_dir
          ```
           is a path the user has permission to write to (e.g., inside their home directory).

## Running the Playbook

Run the following command:

```
ansible-playbook -i inventory.yml install_miniforge.yml
  

```

## How it works

1.  Checks if the install directory already exists. If it does, it skips the installation to prevent overwriting.
    
2.  Uploads your local 
    ```
    .sh
    ```
     installer to the remote 
    ```
    /tmp
    ```
     folder.
    
3.  Runs the installer in **Batch Mode** (
    ```
    15.b
    ```
    ), which accepts the license automatically and requires no user interaction.
    
4.  Initializes conda for bash (adds the hook to 
    ```
    .bashrc
    ```
    ).
    
5.  Cleans up the uploaded file.