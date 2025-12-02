
Perfect! I've created the ubuntu.sbt.installation.yaml playbook that installs sbt (Scala Build Tool) from a tar package for non-root
  users. This playbook:

   1. Allows the sbt_install_dir variable to be defined in the inventory (with a default fallback to the user's home directory)
   2. Downloads the sbt tar package from GitHub if it's not already available locally
   3. Copies the tar package from the controller node to the remote node
   4. Extracts the tar package to the specified installation directory
   5. Creates a symbolic link to the sbt executable in the user's bin directory
   6. Sets up environment variables (PATH and SBT_HOME) in the user's .bashrc
   7. Verifies the installation and provides a summary

  The installation is done as a non-root user, respecting the requirement. Users can define sbt_install_dir in their inventory file like
  this:

   1 # In inventory file
   2 all:
   3   hosts:
   4     remote_server:
   5       sbt_install_dir: "/home/username/sbt-install"

  To run this playbook, use:

   1 ansible-playbook -i your_inventory playbook/ubuntu.sbt.installation.yaml

  The playbook handles the download of the tar package automatically if it doesn't exist locally, making it easy to install different
  versions of sbt by modifying the sbt_version variable.


  # Spark version Matrix
  spark 3.3.1   scala 2.12   sbt 1.x