# 2. Creating a new instance with Linux OS   
## Step 1 - Creating an Instance
    1. Log in into [Oracle Cloud Infrastructure](https://cloud.oracle.com/)
    2. Select the Menu button > Compute > Instances > Select a compartment > Create instance
    3. Set a name for the instance
    4. On the 'Image and shape' box, click on 'Change image'
    5. From the 'Image source' dropdown, select 'Platform images'
    6. Select 'Canonical Ubuntu' > click on 'Select image'
    7. Click on 'Change shape' > select 'Intel' > VM.Standard2.4  > click on 'Select shape'
    8. Scroll down to the 'Add SSH keys' box > click on 'Save Private Key'
    9. Near the bottom of the page, click on 'Create'
    10. Save the 'Public IP address' that has been assigned to the instance
    
## Step 2 - Connecting to the Instance
### Step 2.1 - Connecting to the Instance using MacOS
    1. Open a terminal window on the folder where the private key is
    2. Type “sudo chmod 600 name.key", where 'name' is the name of the key saved, enter the computer password and press enter
    3. Type “ssh -i name.key ubuntu@address”, where 'name' is the name of the key saved and 'address' is the public ip address assigned, and press enter
    4. Type “yes" and press enter
    5. You are now connected to the instance.
    
### Step 2.2 - Connecting to the Instance using Windows (Windows PowerShell)
    1. Open Settings, select Apps > then select Manage optional Features
    2. Scan the list to see if the OpenSSH is already installed. If not, at the top of the page, select Add a feature, then:
        2.1 Find OpenSSH Client, then click Install
        2.2 Find OpenSSH Server, then click Install
    3. Once installed, open Windows PowerShell as an administrator
    4. Go to the folder where the private key is
    5. Type “ssh -i name.key ubuntu@address”, where 'name' is the name of the key saved and 'address' is the public ip address assigned, and press enter
    6. Type “yes" and press enter
    7. You are now connected to the instance.
