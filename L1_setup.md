Typing is one of the CORE skills as a Software developer.

#### [edclub (typingclub.com)](https://www.typingclub.com/sportal/program-3.game)





To install Homebrew on a Mac, follow these steps:</u>**

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

install xcode tools if needed 



**<u>Prerequisites

Before installing Homebrew, ensure that you have the following:

1. **macOS**: Homebrew supports macOS and Linux.

2. Command Line Tools

   : Xcode's Command Line Tools should be installed. You can install them by running the following command in Terminal:

   ```bash
   xcode-select --install
   ```

   This will open a dialog asking if you want to install the tools. Click "Install."

### Installing Homebrew

1. **Open Terminal**: You can open Terminal from the Applications > Utilities folder or by using Spotlight (Cmd + Space and type "Terminal").

2. **Run the Homebrew Installation Script**: Copy and paste the following command into the Terminal and press Enter:

   ```bash
   
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

   This command downloads and runs the official Homebrew installation script.

3. **Follow the On-Screen Instructions**:

   - The script will prompt you for your password. This is required to install Homebrew in `/usr/local`.
   - The installation will download and install Homebrew and any necessary dependencies.

4. **Verify the Installation**: After the installation is complete, you can verify that Homebrew is installed correctly by running:

   ```bash
   
   brew --version
   ```

   This command will display the installed version of Homebrew.

### Using Homebrew

With Homebrew installed, you can use the `brew` command to install, update, and manage packages. For example:

- **To install a package** (e.g., wget):

  ```bash
  brew install wget
  ```

  

- **To update Homebrew and all installed packages**:

  ```bash
  brew update
  brew upgrade
  ```

- **To uninstall a package**:

  ```bash
  brew uninstall wget
  ```

- **To list all installed packages**:

  ```bash
  brew list
  ```

Homebrew provides an easy way to install and manage software packages on your Mac. For more information and a list of available packages, you can visit the [Homebrew website](https://brew.sh).



**<u>Install Java 17</u>**

To install the open-source version of Java 17 using Homebrew on macOS, you can follow these steps:

1. **Open Terminal**: You can open Terminal from the Applications > Utilities folder or by using Spotlight (Cmd + Space and type "Terminal").

2. **Update Homebrew**: It's a good practice to update Homebrew to the latest version before installing new software. You can do this with the following command:

   ```bash
   brew update
   ```

3. **Install Java 17**: Homebrew provides different open-source distributions of Java. The most common distributions are **AdoptOpenJDK**, **Eclipse Temurin**, and **Zulu OpenJDK**. You can choose one based on your preference. Let's install **Eclipse Temurin** as an example:

   ```
   brew install temurin@17
   ```

   This command will install the Eclipse Temurin JDK (formerly known as AdoptOpenJDK) version 17.

4. **Verify the Installation**: After the installation is complete, you can verify that Java 17 has been installed correctly by running:

   ```
   java -version
   ```

   This command should output the version of Java that was installed, confirming that Java 17 is installed and available.

5. **Set Java 17 as the Default (Optional)**: If you have multiple versions of Java installed and want to set Java 17 as the default, you can manage the Java versions using the `java_home` command or Homebrew's `brew` commands. For instance:

   ```
   export JAVA_HOME=$(/usr/libexec/java_home -v 17)
   ```

   You can add this line to your shell profile file (e.g., `~/.bash_profile` or `~/.zshrc`) to make the change persistent.

Install IntelliJ IDEA **<u>Community Edition</u>**

[Download IntelliJ IDEA – The Leading Java and Kotlin IDE (jetbrains.com)](https://www.jetbrains.com/idea/download/?fromIDE=&section=mac)

![image-20240731004541154](/Users/robinbajaj/Library/Application Support/typora-user-images/image-20240731004541154.png)

[Which Version of JDK Should I Use? | whichjdk.com](https://whichjdk.com/)

![image-20240731005427617](/Users/robinbajaj/Library/Application Support/typora-user-images/image-20240731005427617.png)



SDKMan is another popular package manager for Unix/Windows 

[Installation - SDKMAN! the Software Development Kit Manager](https://sdkman.io/install)



