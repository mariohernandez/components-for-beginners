# Local setup

The setup for this training will allow you to follow along with the hands-on exercises during and after the training.

### Training requirements

* macOS 10.14 or higher.  Windows 10 Pro
* A text/code editor.  We recommend [Microsoft Visual Studio Code](https://code.visualstudio.com/download) which works on macOS and Windows.
* A Command Line Interface \(CLI\) tool.  On macOS use [Terminal](https://www.youtube.com/watch?v=Jm8-UFf8IMg), and on Windows use [PowerShell](https://www.youtube.com/watch?v=VFuobJbbDtU)
* Windows users may need PHP installed.  You could use [WampServer](https://www.youtube.com/watch?v=D_Fhu_6RuMw)
* Basic familiarity with [running commands on a CLI ](https://www.hongkiat.com/blog/web-designers-essential-command-lines/)is useful
* Basic understanding of HTML and CSS is required

[Learn command line basics](https://tutorial.djangogirls.org/en/intro_to_command_line/)

### Build Tools needed:

1. NodeJS & NPM \(Read on for instructions on installing\)

## 1. NodeJS & NPM

NodeJS is a modern application-building tool that uses JavaScript to build and run application on a server. Pattern Lab Node Edition is built with NodeJS.

NPM stands for Node Package Manager, and it's a tools that makes it possible to interact with Node to execute tasks and manage node software dependencies.

#### Installing Node & NPM

{% hint style="info" %}
For a video tutorial on how to setup your environment download the [Local Setup for Beginners](https://drive.google.com/drive/folders/1-gIa-bYV1LXhK6t51CWarrX-h1DUvzbO?usp=sharing) video. Or, you can follow the instructions below.
{% endhint %}

* To install Node & NPM download the latest **LTS** package for your Operating System \(Windows or macOS\), from [https://nodejs.org/](https://nodejs.org/en/).  The download package includes both, Node and NPM.

## 2. Creating a Pattern Lab Project

Pattern Lab helps you and your team build thoughtful, pattern-driven user interfaces using [atomic design](http://atomicdesign.bradfrost.com) principles.

#### Installing Pattern Lab

To install and setup Pattern Lab you will need to use a Command Line Interface \(CLI\) tool. A CLI helps you run or execute commands to perform an action.

* Mac users: Use **Terminal**. \(On your Finder's sidebar click **Applications &gt; Utilities &gt; Terminal.app**\)
* Windows users: It is recommended you use **PowerShell**. \(Find it in **Start Menu &gt; All apps,&gt; Windows PowerShell** and tap **Windows PowerShell**\)

### Follow these steps to setup a Pattern Lab project

1. Create a directory or folder called **components\_project** anywhere in your computer for your Pattern Lab project.  A good place for the new directory could be **Documents** on Mac, and **My Documents** on Windows.
2. Open your CLI tool. By default the CLI will open in your computer's home directory.
3. On Mac, type `ls` and press Return.  On Windows, type `dir` and press Enter.  You should see the folder where you created the **components\_project** folder \(i.e. Documents or My Documents\).
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

If everything ran successfully Pattern Lab should had open on your browser. Otherwise see our Troubleshooting guide below.

{% hint style="danger" %}
**DID YOU GET ERRORS?** See our [troubleshooting guide](https://docs.google.com/document/d/1BU5C4jFcUKo2r-YCwT0UH-s4Rfb95KvEnHxCzfnMVF8/edit#).
{% endhint %}

This completes the local computer setup. If you received errors and they don't appear in our troubleshooting guide [please fill out this quick form](https://forms.gle/Xt4aYbCWCrK1zH65A) to submit your error**\(s\)** so we can provide you with possible steps to correct. You could also try searching for the error message on Google or your preferred search engine by copying the error from the command line and pasting into the search engine.

