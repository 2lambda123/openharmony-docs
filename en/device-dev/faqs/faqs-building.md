# Compilation and Building Subsystem


## Mini and Small Systems


### "usr/sbin/ninja: invalid option -- w" Displayed During the Build Process

- **Symptom**
  The compilation fails, and **usr/sbin/ninja: invalid option -- w** is displayed.

- **Possible Causes**
  The Ninja version in the compilation environment is outdated and does not support the **--w** option.

- **Solution**
  Uninstall Ninja and GN in the environment and reinstall them by following instructions in [Obtaining Tools](../get-code/gettools-ide.md).


### "/usr/bin/ld: cannot find -lncurses" Displayed During the Build Process

- **Symptom**
  The compilation fails, and **/usr/bin/ld: cannot find -lncurses** is displayed.

- **Possible Causes**
  The ncurses library is not installed.

- **Solution**
    
  ```
  Run **sudo apt-get install lib32ncurses5-dev** to install the library.
  ```


### "line 77: mcopy: command not found" Displayed During the Build Process

- **Symptom**
  The compilation fails, and **line 77: mcopy: command not found** is displayed.

- **Possible Causes**
  Mcopy is not installed.

- **Solution**
    
  ```
  Run **sudo apt-get install dosfstools mtools** to install mcopy.
  ```


### "riscv32-unknown-elf-gcc: error trying to exec 'cc1': execvp: No such file or directory" Displayed During the Build Process

- **Symptom**
  The compilation fails, and the following information is displayed: **riscv32-unknown-elf-gcc: error trying to exec 'cc1': execvp: No such file or directory**.

- **Possible Causes**
  Permission is required to access files in the **riscv** compiler path.

- **Solution**
    Run the following command to query the directory where **gcc_riscv32** is located:
    
  ```
  which riscv32-unknown-elf-gcc
  ```

  Run the **chmod** command to change the directory permission to **755**.


### "No module named 'Crypto'" Displayed During the Build Process

- **Symptom**
  The compilation fails, and **No module named'Crypto loaded** is displayed.

- **Possible Causes**
  Crypto is not installed in Python3.

- **Solution**
  1. Run the following command to query the Python version:
        
      ```
      python3 --version
      ```
  2. Ensure that Python 3.7 or later is installed, and then run the following command to install pycryptodome:
        
      ```
      sudo pip3 install pycryptodome
      ```


### "xx.sh : xx unexpected operator" Displayed During the Build Process

- **Symptom**
  The compilation fails, and **xx.sh [: xx unexpected operator** is displayed.

- **Possible Causes**
  The compilation environment is shell instead of bash.

- **Solution**
    
  ```
  sudo rm -rf /bin/sh
  sudo ln -s /bin/bash /bin/sh
  ```


### "Could not find a version that satisfies the requirement six&gt;=1.9.0" Displayed During the Build Process

- **Symptom**
  The following error occurs during compilation and building:

    
  ```
  Could not find a version that satisfies the requirement six>=1.9.0
  ```

- **Possible Causes**
  **six** is not installed.

- **Solution**
  Solution 1: Run the **pip3 install six** command to install **six** online.

  Method 2: Offline installation

  Download the installation package from [PyPI](https://pypi.org/project/six/#files).

  ![en-us_image_0000001251276115](figures/en-us_image_0000001251276115.png)

  Save the source code to the Linux server and run the **pip3 install six-1.14.0-py2.py3-none-any.whl** command to install **six**.

  After the preceding installation is complete, rebuild an environment.


### "cannot find -lgcc" Displayed During the Build Process

- **Symptom**
  The following error occurs during the build process:

    
  ```
  riscv32-unknown-elf-ld: cannot find -lgcc
  ```

- **Possible Causes**
  The PATH is incorrectly written by **gcc_riscv32**. There is an extra slash (/).

    
  ```
  ~/gcc_riscv32/bin/:/data/toolchain/
  ```

- **Solution**
  Modify the PATH by deleting the slash (/).

    
  ```
  ~/gcc_riscv32/bin:/data/toolchain/
  ```


### The Message Indicating Python Cannot Be Found Is Displayed During the Build Process

- **Symptom**
  The following error occurs during the build process:

    
  ```
  -bash: /usr/bin/python: No such file or directory
  ```

- **Possible Cause 1**
  Python is not installed.

- **Solution**
  Run the following command to install Python. The following uses Python 3.8 as an example.

    
  ```
  sudo apt-get install python3.8
  ```

- **Possible Cause 2**
  The soft link that points to the Python does not exist in the **usr/bin** directory.

  ![en-us_image_0000001243200677](figures/en-us_image_0000001243200677.png)

- **Solution**
  Run the following commands to add a soft link:

    
  ```
  # cd /usr/bin/ 
  # which python3
  # ln -s /usr/local/bin/python3 python
  # python --version
  ```

  Example:

  ![en-us_image_0000001243320787](figures/en-us_image_0000001243320787.png)


### The Message Indicating Python 3 Cannot Be Found Is Displayed During the Build Process

- **Symptom**

  ![en-us_image_0000001251276255](figures/en-us_image_0000001251276255.png)

- **Possible Causes**
  Python 3 is not installed.

- **Solution**
  Run the following command to install Python 3:

    
  ```
  sudo apt-get install python3.8
  ```
