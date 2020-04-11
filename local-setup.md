# Local setup

The local computer setup for this training will allow you to follow along with the hands-on exercises.  You need to install the following two tools:  NodeJS & NPM

{% hint style="info" %}
For a video tutorial on how to setup your environment download the [Local Setup for Beginners](https://drive.google.com/drive/folders/1-gIa-bYV1LXhK6t51CWarrX-h1DUvzbO?usp=sharing) video.  Or, you can follow the instructions below.
{% endhint %}

### 1. NodeJS & NPM

Node is a JavaScript runtime.  Node.js is designed to build scalable network applications and it is required by Pattern Lab Node Edition.  

#### Installing Node & NPM

* To install Node & NPM download the latest **LTS** package for your Operating System \(Windows or macOS\), from [https://nodejs.org/](https://nodejs.org/en/).  The download package includes both, Node and NPM.

### 2. Creating a Pattern Lab Project

Pattern Lab helps you and your team build thoughtful, pattern-driven user interfaces using [atomic design](http://atomicdesign.bradfrost.com) principles.

#### Installing Pattern Lab

To install and setup Pattern Lab you will  need to use  a command  line tool.  In Mac you can use **Terminal**, and in Windows it is recommended you use **PowerShell**.

1. Create a directory or folder anywhere in your computer where you want to setup your Pattern Lab project for this training.  You can call this directory anything you wish \(i.e. **components\_project**\).
2. In your command line tool, change into the directory you created above by typing a command like the one below and pressing **Return**: \(_If your directory name is different than **components\_project**, use the name of your directory\)._

   ```text
   cd components_project
   ```

3. Once you are in the directory you created, type this command and press **Return**

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

This completes the local computer setup.  If you received errors that your project did not complete successfully, you can google the error message you are getting for possible solutions, or, you can contact us for assistance.

