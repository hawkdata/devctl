Perfect! I've created the ubuntu.rust.installation.x86.yaml playbook that installs Rust and Cargo from the official installer for non-root users. This playbook:

  1. Allows the rust_install_dir variable to be defined in the inventory (with a default fallback to ~/rust in the user's home directory)
  2. Downloads the official Rust installation script from rustup.rs
  3. Runs the installer to install Rust and Cargo in the specified directory using rustup
  4. Configures the default toolchain and sets up environment variables (RUSTUP_HOME, CARGO_HOME, and PATH) in the user's .bashrc
  5. Verifies the installation and provides a summary

  The installation is done as a non-root user, respecting the requirement. Users can define rust_install_dir in their inventory file like this:

   1 # In inventory file
   2 all:
   3   hosts:
   4     remote_server:
   5       rust_install_dir: "/home/username/custom-rust-install"

  To run this playbook, use:

   1 ansible-playbook -i your_inventory playbook/ubuntu.rust.installation.x86.yaml

  The playbook downloads the official Rust installer script, runs it to install Rust and Cargo with rustup, configures the default toolchain, and properly configures the environment variables needed for Rust development.