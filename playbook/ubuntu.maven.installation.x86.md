Perfect! I've created the ubuntu.maven.installation.x86.yaml playbook that installs Apache Maven from a tar package for non-root users. This playbook:

  1. Allows the maven_install_dir variable to be defined in the inventory (with a default fallback to the user's home directory)
  2. Copies the Maven tar package from the controller node to the remote node
  3. Extracts the tar package to the specified installation directory
  4. Sets up environment variables (PATH and MAVEN_HOME) in the user's .bashrc
  5. Verifies the installation and provides a summary

  The installation is done as a non-root user, respecting the requirement. Users can define maven_install_dir in their inventory file like this:

   1 # In inventory file
   2 all:
   3   hosts:
   4     remote_server:
   5       maven_install_dir: "/home/username/maven-install"

  To run this playbook, use:

   1 ansible-playbook -i your_inventory playbook/ubuntu.maven.installation.x86.yaml

  The playbook copies the Maven tar package from the controller to the remote node, extracts it, and sets up the environment variables needed for Maven to function properly.