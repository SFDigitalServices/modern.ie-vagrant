# modern.ie-vagrant

Modern.ie for Vagrant 

To create a new Modern.IE box:
   * Clone this repository
   ```bash
   $ git clone https://github.com/hugsy/modern.ie-vagrant.git win7
   ```  
   * Edit `Vagrantfile` to change the line `VM = VMS[<id>]` where `id` is the index of the box you want to have (default: `Windows 7 / IE11`)
   * For the directory, launch Vagrant the first time with the environment `FIRSTBOOT` set to `1`
   ```bash
   $ cd win7 && FIRSTBOOT=1 vagrant up 
   ```
   _NOTE_: the `FIRSTBOOT` will force Vagrant to show a GUI for the VM, which is required to run the initial scripts and enable WinRM
   * (XP only) WinRM must be installed first, so install the .Net Framework 2.0 then the KB968930 (both in `installers\xp`) 
   * (Vista+) When Windows prompts for the type of network for the new interface, choose either `Home` or `Work` (`public` will make the firewall block 
   all WinRM communications)
      * Win7 : https://support.microsoft.com/en-ca/help/2578723/windows-7-network-connections-are-stuck-in-public-mode
      * Win8 & 10 : https://www.online-tech-tips.com/windows-10/change-from-public-to-private-network-in-windows-7-8-10/
   * Finally then execute as Administrator `scripts\RunFirstBoot.bat` (can be found under 
   `\\vboxsrv\vagrant\scripts\RunFirstBoot.bat`)
   
The next boot can be done without the `FIRSTBOOT` environment variable, WinRM and RDP will work properly. 
   
That's it!!


## SFDS notes
```bash
git clone git@github.com:SFDigitalServices/modern.ie-vagrant.git win7
cd win7 && FIRSTBOOT=1 vagrant up
```
You only need FIRSTBOOT=1 when running for the first time.

##### Access local Lando dev environment with Internet Explorer
Find out what port lando is running on.  The port is randomly assigned by Docker on every start.  Look for the urls of edge service.
```bash
lando info
```
Look for something like:
```bash
  "edge": {
    "type": "varnish",
    "version": "4.1",
    "hostnames": [
      "edge",
      "edge.sfgov.internal"
    ],
    "vcl": "/Users/joshchou/.lando/services/config/pantheon/pantheon.vcl",
    "backends": [
      "nginx"
    ],
    "urls": [
      "http://localhost:32814",
      "http://sfgov.lndo.site:8000",
      "https://sfgov.lndo.site"
    ]
  },
```

In IE, go to the network port you just discovered, with ip address of 10.0.2.2.  For example http://10.0.2.2:32814/