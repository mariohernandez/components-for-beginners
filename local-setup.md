# Local setup

The local computer setup for this training will allow you to follow along with the hands-on exercises.  

### Tools needed:
1. A text editor for writing code.  We recommend [Microsoft Visual Studio Code](https://code.visualstudio.com/download).  This works on Mac and Windows.
2. NodeJS & NPM (Read on for instructions)

## 1. NodeJS & NPM

Node is a JavaScript runtime.  Node.js is designed to build scalable network applications and it is required by Pattern Lab Node Edition.  

#### Installing Node & NPM

{% hint style="info" %}
For a video tutorial on how to setup your environment download the [Local Setup for Beginners](https://drive.google.com/drive/folders/1-gIa-bYV1LXhK6t51CWarrX-h1DUvzbO?usp=sharing) video.  Or, you can follow the instructions below.
{% endhint %}

* To install Node & NPM download the latest **LTS** package for your Operating System \(Windows or macOS\), from [https://nodejs.org/](https://nodejs.org/en/).  The download package includes both, Node and NPM.

## 2. Creating a Pattern Lab Project

Pattern Lab helps you and your team build thoughtful, pattern-driven user interfaces using [atomic design](http://atomicdesign.bradfrost.com) principles.

#### Installing Pattern Lab

To install and setup Pattern Lab you will need to use  a Command Line Interface (CLI) tool. A CLI helps you run or execute commands to perform an action.

* Mac users: Use **Terminal**. (Find it in **Applications > Utilities > Terminal.app**)
* Windows users: It is recommended you use **PowerShell**. (Find it in **Start Menu > All apps,> Windows PowerShell** and tap **Windows PowerShell**)

### Follow these steps to setup a Pattern Lab project
1. Create a directory or folder called **components\_project** anywhere in your computer for your Pattern Lab project.  A good place for the new directory could be **Documents** on Mac, and **My Documents** on Windows.
2. Open your CLI tool. By default the CLI will open in your computer's home directory.
3. On Mac, type `ls` and press Return.  On Windows, type `dir` and press Enter.  You should see the folder where you created the **components_project** folder (i.e. Documents or My Documents).
4. In your CLI, type `cd Documents` or `cd MyDocuments` and press Return.
5. On Mac, type `ls` and press Return.  On Windows, type `dir` and press Enter.  You should see `components_project`
6. Type `cd components_project` and press Return.
7. Once you are in the directory you created, type this command and press **Return**

   ```text
   npm create pattern-lab
   ```

Respond to the on-screen prompts as follows:

* Press **Return** when asked to specify a directory for your Pattern Lab project.  Pressing Return  indicates you want to use the current directory or folder you are currently in
* For _Templating language_ select **Twig \(PHP\)** and press  **Return**
* When asked _What initial patterns you want to include_ select **Twig \(PHP\) demo patterns \(full demo website and patterns\)** and press **Return**
* Type **Y** and press **Return** when asked if you are happy with your choices.  Pattern Lab will start  installing and setting up your project.  This could take a few minutes. **Do not interrupt it**.
* Finally, if you want to look at your Pattern Lab project, run this command and press **Return**

   ```text
   npm start
   ```

This completes the local computer setup.  If you received errors indicating your project did not complete successfully, you can google the error message you are getting for possible solutions, or, you can contact us for assistance.
