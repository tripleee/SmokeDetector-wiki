# Setting up SmokeDetector

## Basic setup

To set up SmokeDetector (SD), please execute the following commands:

```
git clone https://github.com/Charcoal-SE/SmokeDetector.git
cd SmokeDetector
git config user.email "smokey@erwaysoftware.com"
git config user.name "SmokeDetector"
git checkout deploy
sudo pip3 install -r requirements.txt --upgrade
pip3 install --user -r user_requirements.txt --upgrade
```

Next, copy `config.sample` to a new file called `config`, and edit the values required. If you are going to be running this SmokeDetector instance as a normal SD instance with metasmoke, see [the "config" file with MS](#user-content-the-config-file) below.

You should now be able to [run SmokeDetector](#user-content-running-smokedetector).

## Running SmokeDetector with metasmoke
You will need a [keybase](https://keybase.io/) account. You will also need to have the "smoke detector runner" role on metasmoke (MS). Contact an MS admin to request the role. When given the role, you should separately be added to the "charcoal" channel on keybase.

### The "config" file with MS
In the files section for the keybase "charcoal" channel, there is a "config" file. You should use that config file as a basis for the "config" file you use in your "SmokeDetector" directory. 
* Set `location` to the name you choose for your SD instance. This should be your username, followed by a slash and an identifier that's unique among all your Smokey instances. This is the name that your instance will display in messages in chat and what will be displayed on MS for status.
* Set `metasmoke_key`  
  * On metasmoke in the dropdown for your username, select "My SmokeDetectors".
  * Click on "create a new key" and enter the name you used for `location` above.
  * Once you complete the dialog, your SD instance will be listed and you can copy the "Key" to `metasmoke_key`.
* Save the "config" file, as those are the only changes you need.

### Run SmokeDetector
At this point, you should be able to [run SmokeDetector using the instructions below](#user-content-running-smokedetector).

## Setting up an AWS EC2 linux instance for SmokeDetector
Using a AWS EC2 instance can be a quick way to get an SD instance up and running. Based on reports from @iBug in chat, a t2.micro instance, what's available from the AWS Free Tier for 12 months, doesn't have enough CPU credits for the instance to be the active SD instance full-time. It's expected that a t3.micro, which actually costs less than a t2.micro, once past the free period, should be sufficient for a full-time active SD instance. However, a t2.micro instance does appear to be enough for SD to run as a standby instance to fill in on an irregular basis.

To set-up a t2.micro instance for SD you can do the following:
* Create the EC2 instance ([launch a AWS instance tutorial](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/))
  * Create an AWS account (address, verifiable phone number, and credit card required) and Sign-in to the AWS console.
  * Click "Launch Instance ->"
  * Click "Select" for "Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type - ami-0cd3dfa4e37921605" (the first one in the list)
  * Click "Review and Launch"
  * Click "Launch"
  * Create a public key pair, or use one you've previously created.
    * If creating a new public key pair, download the private key to somewhere on your system from which you can run `ssh`.
  * Click "View Instances"
  * Select the new instance
  * Click "Connect"
  * Use ssh to connect to EC2 instance:
    * Copy-&-paste the example ssh line in the popup into a command line running in the directory where you stored the .pem file with the private key (created or selected earlier).
* Execute the following commands (you can copy-&-paste all of them at one time):

        sudo yum -y update
        sudo yum -y install gcc
        sudo yum -y install git
        sudo yum -y install python36
        sudo yum -y install python36-devel
        sudo python3 -m pip install pip --upgrade

        git clone https://github.com/Charcoal-SE/SmokeDetector.git
        cd SmokeDetector
        git config user.email "smokey@erwaysoftware.com"
        git config user.name "SmokeDetector"
        git checkout deploy
        sudo /usr/local/bin/pip3 install -r requirements.txt --upgrade
        pip3 install --user -r user_requirements.txt --upgrade

* Create the "config" file
  * See [The "config" file with MS](#user-content-the-config-file) above if you are going to use this SD instance with metasmoke.
  * If you are not going to run this SD instance with metasmoke, then copy `config.sample` to a new file called `config`, and edit the values required.

# Running SmokeDetector
To run, use `python3 nocrash.py`, or `python3 nocrash.py standby` (preferably in a daemon-able mode, like a `screen` session).
You can also use `python3 ws.py`, but then SmokeDetector will be shut down after 6 hours;
when running from `nocrash.py`, `ws.py` will automatically be restarted.
(This is to be sure that closed WebSockets, if any, are reopened.)

#### `nocrash.py`
`nocrash.py` is the controlling Python code for SmokeDetector. It runs `ws.py`, which is the SD instance, in a sub process and restarts it when it stops. `ws.py` may stop as the result of `!!/` commands given to SD in chat, or do to errors. The syntax for `nocrash.py` is:

    nocrash.py [standby]

The `standby` option starts the SD instance in [standby mode](https://github.com/Charcoal-SE/SmokeDetector/wiki/SmokeDetector-Statuses#standby-mode).


<sub>Portions of this page were taken from [README.md](https://github.com/Charcoal-SE/SmokeDetector/blob/master/README.md).</sub>
