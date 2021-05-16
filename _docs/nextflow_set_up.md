

# Nextflow step up 
Please make sure to have these essential softwears installed before running or developing on Nextflow. In this wikipage you'll find the instructions to get you and your machine set up with these tools. 

Check list of key tools to develop or run pipelines in Nextflow. 

- [ ] iTerm2
- [ ] HomeBrew
- [ ] GitHub 
- [ ] GitKraken
- [ ] Docker 
- [ ] VSC code and extensions
- [ ] JAVA
- [ ] Nextflow 


## Terminal 
You would need to use terminal commands to run Nextflow and to install the majority of the required tools.   
If you are on a Mac we reccomend using [iTerm2](https://iterm2.com/) instead of the default terminal.  
Windows alternative?

## Installing Homebrew: 
**Homebrew** is a free and open-source software package management system that simplifies the installation of the softwares you'll need to run Nextflow.  
Homebrew is compatible with Apple's operating system macOS as well as Linux.  
Paste the following into a macOS terminal or Linux shell prompt:  
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`  
This script installs Homebrew to `/usr/local`for macOS Intel, `/opt/homebrew `for Apple Silicon, so that you don't need to type "sudo" to install packages.
The script will ask you to confirm each time it install a software package.  
If you are using macOS, make sure you have command line tools (CTL) for Xcode installed. If not, type the following code before installation:
`xcode-select --install`

## Version Control and Reproducibility tools
### GitHub
Similarly to other programming models, Version control is an essential practice to track and manage changes when developing on Nextflow. 
Especially when multiple developers/teams work together on the same project, as we do in our Hackathons.   
Therefore you should first create a [Github account](https://github.com/) and then provide your github account to a lab member in order to have access to our [Luslab GitHub account](https://github.com/luslab/luslab.github.io)

You can find more info on Version Control and GitHub on our dedicated wiki pages on [reproducibility](https://luslab.github.io/reproducibility/intro/) and [git](https://luslab.github.io/reproducibility/git/)

### GitKraken
Once you have a gitHub account, we suggest using the Git GUI [GitKraken](https://www.gitkraken.com/) to graphically visualize the history and changes to your repos,  which offers a more intuiive approach to working with Git.
Download [Here](https://www.gitkraken.com/download) the free GitKraken desktop version (Mac, Windows or Linux). 
Once installed, syncronise GitKraken with your GitHub account. 

### Installing Docker 
Nextflow supports **Docker** and **Singularity** containers technology.
**Docker** can package an application and its libraries and other dependencies in a virtual container. This maximise reproducibility and portability as the applications in the virtual container can then be accessed and run on any other Linux, Windows, or macOS machine regardless of any customized settings.  

To install Docker from the command line, type the following command in Homebrew to download the Docker package and run the installer:  
`brew cask install docker`   
To make sure the installation was succesful, type:`docker --version`  
If the command returns your Docker version, the installation was succesful.   
If the command does not return a version, try starting Docker daemon:   
Type "Docker" in Sporlight on mac or in the Application folder in Finder.  
Click the icon to run Docker deamon and then try the installation again.  

Docker desktop? 


### Installing VSC code 
download the following extension: 
- Docker 
- Nextflow 
- Java (?)



### Setting up your dev directory 

Create new `dev` repository in home directory. This `dev` repository will be a container for nexflow script developing 
Inside `dev` create the `repos` and `test` directories 

### Cloning your first directory 
Now you are ready to clone any directory from github into your `dev` folder. 
How to clone with git Kraken: 
open git Kraken and click on `clone a repo`, here you can either clone a directory from a given URL or directly from git hub 
Cloning will automatically clone an external directory and its content into your home-direcotry folder. 





### Installing Java
Nextflow requires Java to be installed first. 
Use Home brew to install Java by following the instructions here https://devqa.io/brew-install-java/
 Did we installed java in usrbin???
`brew install cask java`
`ls -lsa /usr/local/Cellar/openjdk/`
`ls -lsa /usr/local/opt/openjdk`
`sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk`
`java -version`



### Installing Nextflow

open your terminal and create a new directory called "usrbin": 
`mkdir usrbin`
`cd usrbin`
then run: `wget -qO- https://get.nextflow.io | bash`
This will create a main nextflow file in your current directory.
You may want to move this nextflow file to a different directory that is accessible by your $PATH variable, 
or add your current directory to your $PATH with export. 
First, check what directories are in your current $PATH variable by typing:
`echo $PATH`
If the output doesn't include the directory containing your main nextflow file, you can either move this file to an
existing path (by draggin and dropping) or you can add the directory containing this file to your path variable with export:
`sudo nano /etc/paths` then type `export PATH=$PATH:/my/custom/path`,
`echo "$PWD"`
This command should now return the path to your directory, containing the main nextflow file.
Check if the installation was successful by typing:
`nextflow -version`
If the command returns a version number, the installation was succesful.

#iTerm commands used: 
`conda install graphviz`
`docker build -f ./Dockerfile -t luslab/char-hicexplorer:latest .`




