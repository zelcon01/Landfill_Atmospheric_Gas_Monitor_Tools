# Setup Guide

Welcome to the setup guide for the Remote Landfill Gas Monitoring Tools. This guide will walk you through the necessary steps to set up and configure the environment for working with this project. 

# Contents

1. [Anaconda Navigator](#anaconda-navigator)
2. [Creating a Conda Environment](#creating-a-conda-environment)
3. [Setting up Jupyter Lab](#setting-up-jupyter-lab)
4. [OpenEO setup using Anaconda Navigator](#openeo-setup-using-anaconda-navigator)
5. [OpenEO setup using PyPi](#openeo-setup-using-pypi)
6. [Registering with Copernicus Data Space Ecosystem](#registering-with-copernicus-data-space-ecosystem)
7. [Authentication with OpenEO](#authentication-with-openeo)

---

## Anaconda Navigator

Anaconda Navigator, containing Python and additional tools, includes ‘Conda’, a package manager for creating shareable environments with necessary packages. This includes Jupyter Lab for running Python code. This will be installed first. To download Anaconda, navigate to https://docs.anaconda.com/anaconda/install/ and follow the instructions of your associated operating system. 

## Creating a Conda Environment

In the Anaconda Navigator side bar, click the ‘Environments’ tab. You will see the installed packages (fig.1). 

Figure 1: Environments tab of Anaconda Navigator with environments tab and import button highlighted in red.

Next click on the imports tab (fig.1) and select the file ‘environment.yml’ contained in the .zip file of the tool’s download, choosing an appropriate name for the environment (fig.2). 

Figure 2: The import config box (left) and the contents of ‘environment.yml’ (right).

Click Import. Depending on the connection speed of your network, the process of installing all the packages may take several minutes. Once finished you will be returned to the environments tab (fig.1) 
Next click on the ‘Home’ tab in Anaconda Navigator’s sidebar (fig.3).

Figure 3: Anaconda Navigator with home tab and environment switching dropdown in red.

## Setting up Jupyter Lab

A configuration file (‘.config’) needs to be created  to change the settings used by Jupyter Lab by default. Launch the CMD.exe prompt (fig.4)

Figure 4: Highlighted locations of selected environment and CMD.exe Prompt

In the command prompt, enter the command:

> ```
> jupyter lab --generate-config
> ```
This will create a new folder in your user directory called ‘.jupyter’ containing a python script juptyer_lab_config.py. On Windows this is usually ‘C:\Users\<your_username>’.
Jupyter lab will by default open in your user directory. Unfortunately due to security restrictions it is not possible to navigate to the parent directory of the launch location. So if Jupyter launches in ‘C:\Users\RockyBalboa, it is not possible to move to ‘C:\Users’ or, ‘C:\EGM722’. If the directory you are keeping your data in is outside your user directory, you will need to change the default opening folder to your data directory. 
If your data directory is in your user directory, you should be able to click and navigate there using the interface of Jupyter Lab. If that is not the case, you will need to do the following: 
Open an Anaconda Navigator CMD.exe prompt and type the following command: 

> ```
> jupyter --paths
> ```

This will show something like figure 5 although your file paths will be unique to you. 

Figure 5: results of ‘jupyter –paths’ command showing path used by environment highlighted in red.

The ‘jupyter_lab_config.py’ file mentioned earlier needs to be copy pasted into that folder. 
Once ‘jupyter_lab_config.py’ file has been moved, open it in Notepad++, Visual Studio Code or if you don’t have those, Notepad. Using the shortcut ‘CTRL + F’ type in the following line: ‘c.ServerApp.root_dir’ (without quotes) and you should find the section highlighted in figure 6. 

Figure 6: location of 'c.ServerApp.root_dir' in jupyter_lab_config.py

Remove the ‘#’ and space from the start and add the path used by your environment between the quote marks, adding a ‘r’ beforehand (fig.7). 

Figure 7: path to data directory added to jupyter_lab_config.py

Save and close this file and return to the Anaconda Navigator ‘Home’ tab. Launch Jupyter Lab and if you have followed the steps correctly, you should see that your data directory is automatically displayed (figure 8).

Figure 8: Jupyter Lab showing by default the data directory

## OpenEO setup using Anaconda Navigator

OpenEO is an open-source API that allows access to the earth observation satellite missions run by the Copernicus program. These include the satellites used by this tool. 
First search in the Anaconda Navigator environments tab for ‘openeo’. Make sure that ‘Not installed’ is selected (fig.9). If the package appears here, click its tick box and select apply. If you can’t see it here, please go to section 2.5.

Figure 9: installing OpenEO from Anaconda Navigator.

Next you will be presented with the following screen (fig.10). One this has finished processing the request. Simply click ‘apply’ to begin the installation. 

Figure 10: Anaconda Navigator package installer loading screen.



## OpenEO setup using PyPi

If Anaconda Navigator cannot find OpenEO you can use PyPi, the official third-party software library for Python. Search for ‘pip’, selecting the appropriate tick-box and then clicking apply (fig.11), then clicking apply once the install packages prompt has finished loading (fig.10). 

Figure 11: Installing pip via Anaconda Navigator

Open an Anaconda Navigator CMD.exe prompt and type the following command:

> ```
> pip install openeo
> ```

Once the resultant process has completed, you can close the CMD.exe prompt window. 

## Registering with Copernicus Data Space Ecosystem

Accessing and analysing OpenEO data requires an authentication. To do this, you need to complete a Copernicus Data Space Ecosystem Registration. Go to https://dataspace.copernicus.eu/ and click the green login button (fig.12)

Figure 12: Copernicus Dataspace landing page with login button highlighted in red.

Next click the green ‘register’ button (figure 13):

Figure 13: Copernicus Dataspace sign in page.

On the following page, fill out the application form and then at the bottom click the green ‘register’ button (fig.14). 

Figure 14: End of Copernicus registration page with register button highlighted in red.

Once registered, you will receive an email asking to verify your address. You can then log-in with your email and chosen password. 
For any registration problems, email: help-login@dataspace.copernicus.eu

## Authentication with OpenEO

The very first time one of the tools are run, the following section of code…

> ```
> connection = openeo.connect(url="openeo.dataspace.copernicus.eu")
> connection.authenticate_oidc()
> ```

… will provide you with a URL that will look something like this:

> ```
> Visit https://auth.example.com/device?user_code=EAXD-RQXV to authenticate.
> ```