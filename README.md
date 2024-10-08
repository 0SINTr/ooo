![ooo](img/ooo.png)
# OSINT OpSec Outline
**OOO - Framework for OSINT hygiene**

[![Stable Release](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/0SINTr/ooo/releases/tag/v1.1.0)
[![Last Commit](https://img.shields.io/github/last-commit/0SINTr/ooo)](https://github.com/0SINTr/ooo/commits/main)

Framework for maintaining proper **digital hygiene** whilst performing OSINT-related tasks and investigations.\
This approach is a highly curated checklist of actions that should enhance your own personal and digital security prior to starting any OSINT investigation online.

A few **considerations** before diving in:

* The framework is not an end all be all, and can definitely be improved.
* It's relatively easy to implement in about an hour or so even if you're not a tech god.
* It's completely free, as in the required tools are free of charge and open-source.
* I am in no way affiliated with any of the tools or services discussed below.

**Important note:** The task list below is not exhaustive and more advanced tools and techniques can be employed, however I wanted this framework to be accessible to as many OSINT people as possible. Keep in mind that **journalists**, **private investigators** and **whistleblowers** can be OSINTers too, so not everyone is a cybersecurity or Linux wizard.

## 🎯 **OOO GOALS**

Protecting your **identity**, reducing your **digital footprint** and **keeping you and your data safe** from malware and trackers while performing OSINT work.

## 🚦 OOO Principles

First and foremost, the OOO logic is based on **two fundamental principles**:

1. You should always **keep your real digital identity completely separate from your OSINT-er identity**.
2. You should always **keep every OSINT investigation separate from other investigations**, and also from your OSINT-er identity.

**No ifs, buts and maybes.** 

With these principles in mind, I'm going to start with some advice for each of them:

1. **For following the 1st principle**, you should have a **separate machine** (e.g. laptop) dedicated only for your OSINT-er identity - let's call it the **BASE**. Ideally, it should be a brand new one. Keep in mind that you won't need the latest and greatest hardware on this machine, just a decent+ configuration to run Linux and a VM on top of it. The second option is to re-purpose a machine you already own (maybe an older laptop) specifically for OSINT tasks, however make sure to make a backup and then fully format it before moving on with this framework.
2. **For following the 2nd principle**, you're going to need **virtualization software** (e.g. VirtualBox) installed on your dedicated machine, in which you're going to run VMs. You need a separate VM for **every** OSINT investigation to further keep your specific OSINT tasks, accounts and personas separate from your base OSINT-er setup. Again, different OSINT investigations means different VMs, keeping each investigation contained in its own sandbox, preventing any kind of malware or data leaks to other VMs or to the **BASE** (host) machine.

Now, the list that follows is by no means exhaustive, but it does contain most of the necessary precautions when it comes to securing and keeping the **BASE** safe.

## 🛠️ Task #1 

On your **BASE** machine, start fresh by installing Ubuntu 24.x. If you prefer other Linux distros, go ahead and install your favorite one, however this framework assumes Ubuntu as the OS. For the installation you'll need to download the [latest Ubuntu Desktop .iso image](https://ubuntu.com/download/desktop), then make a bootable USB drive with [Balena Etcher](https://etcher.balena.io/).

During the installation (mode Interactive), pay close attention to the following settings:

* Choose **Default Selection** (not Extended) when asked about what apps and features to install.
* For disk management, choose **LVM & encryption** to fully encrypt your disk. This will protect your data in case of unauthorized physical access to the **BASE** machine. Set a **strong password** during this step. Each time you're going to power on your **BASE** machine, you're going to be prompted to enter this password for decryption.
* When creating your user during installation, first of all do **NOT** name it using your real name, secondly set a **strong password** which is **different** than the password you configured during the previous step. Each time you're going to power on your **BASE** machine, you're going to be prompted to enter this password after entering the password for decryption. Also useful when you walk away from your **BASE** for quickly locking the system.
* For more details regarding the installation process refer to [Ubuntu's official installation guide](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview).

## 🛠️ Task #2

After the installation is complete, make sure your **system is up to date**. In the **Terminal** run:

`sudo apt update && sudo apt upgrade -y`

## 🛠️ Task #3

Enable Ubuntu's default firewall, **ufw**, and set the basic policies for incoming and outgoing traffic.

`sudo ufw default deny incoming`

`sudo ufw default allow outgoing`

`sudo ufw enable`

Your firewall is now active. Check its **status** using:

`sudo ufw status verbose`

**NOTE:** Popular alternatives to **ufw** include [**firewalld**](https://firewalld.org/) and [**OpenSnitch**](https://github.com/evilsocket/opensnitch).

## 🛠️ Task #4

Installing and using a **VPN** for protecting your Internet traffic. This **safeguards your traffic from your ISP** and also **masks your real public IP** when online.

My go-to option is [Proton VPN](https://protonvpn.com/), which is free, open-source, has a strict no-logs policy and it's based in Switzerland under heavy privacy laws. You can also choose to go with the paid version for additional features, however the free version will do. You won't probably ever need cutting-edge Internet speeds on your **BASE** machine or the VMs on top, so **the main goal is the privacy that the VPN provides**, not the speed.

If you prefer other options for your VPN service, that's ok. **Just make sure you always use one**.

* With the free Proton VPN option, you need to create an account before you download it. Do **NOT** use your own Proton account/email, if you already have one for personal use. Create a **new account and email address that has no reference to your real name**, it's free and it takes 10 seconds to do so. You're going to need this email address and password for using your VPN.

* Once you install Proton VPN on your **BASE** machine and log in with your new account, make sure to go to **Settings** and, under **Features**, enable **Kill switch** and check the **Advanced** option. This will **only** allow Internet access over the VPN connection. Also, down below in the **Settings** check the **General** section and, optionally, set a preferred server in the **Auto connect** field. This will make sure that Proton VPN will always connect to that specific server.

* To **make sure your VPN is enabled at startup**, in your Ubuntu search for **Startup Applications**. A new windows opens up, click on **Add**, provide a **Name:** (e.g. ProtonVPN), then click **Browse...** and locate the Proton VPN app - this should be located at **/usr/bin/protonvpn-app**. Once this path appears in the **Command:** field, hit **Save**. Next time you restart Ubuntu your VPN will start automatically. For other VPNs the app location might differ.

## 🛠️ Task #5

Maintaining your passwords and highly sensitive data protected with a **password manager**.

Here are a few good options which are **free** and **open-source**:

* [Bitwarden](https://bitwarden.com/download/)
* [KeePassXC](https://keepassxc.org/download/#linux)
* [ProtonPass](https://proton.me/pass/download)

I won't go into the details of configuring and using each of them because this can be easily found on their websites. 

However, if you choose to stick with the Proton suite and use ProtonPass, keep in mind that it can be easily installed as a **browser extension** and used after logging in with your new Proton email and password. One thing to remember is once you installed the extension, make sure to go to its **Settings**, then in the **Security** tab check the **Extra password** option and set a password that will be required to use ProtonPass. This acts as an additional layer of protection for your sensitive data such as login information.

## 🛠️ Task #6

Let's move on to the **browser** on your **BASE** machine. By default, Ubuntu comes with **Firefox**. Stick with it, no reason to install Chrome or anything else. Needless to say, you should **keep your Firefox updated**. 

Next, it's time to make our **Firefox** more secure. Go to **Settings**.

**General**:

* Make **Firefox** your **default browser**
* Under **Startup**, uncheck: **Open previous windows and tabs**
* Under **Downloads**, check: **Always ask you where to save files**
* Under **Language** uncheck: **Check spelling as you type**
* Under **Browsing**, uncheck **everything**

**Home**:

* Under **New Windows and Tabs**, set **Blank Page for both options**
* Under **Firefox Home Content**, uncheck **everything**

**Search**:

* Under **Default Search Engine**, choose **DuckDuckGo**
* Under **Search Suggestions** and **Address Bar**, uncheck **everything**

**Privacy & Security**:

* Under **Enhanced Tracking Protection**, choose **Strict**
* Under **Website Privacy Preferences**, check **both options**
* Under **Cookies and Site Data**, check: **Delete cookies and site data when Firefox is closed**
* Under **Passwords**, uncheck **everything**
* Under **History**, choose Firefox will: **Use custom settings for history**
* Also under **History** (custom), uncheck **everything** except: **Clear history when Firefox closes**
* Under **Permissions**, go to **Settings...** for each item and check **Block new requests...** then **Save Changes**
* Also under **Permissions**, check **Block pop-up windows** and **Warn you when websites try to install add-ons**
* Under **Firefox Data Collection and Use**, uncheck **everything**
* Under **Security/Deceptive Content**, check **everything**
* Under **Security/Certificates**, check **Query OCSP responder servers...**
* Under **Security/HTTPS-Only Mode**, check **Enable HTTPS-Only Mode in all windows**
* Under **DNS over HTTPS**, check **Max Protection**, then **Choose provider**: **NextDNS**

Now your Firefox is much more secure and should keep you safe from most nasty things out there.

## 🛠️ Task #7

After configuring your Firefox, you can add an extra guardian that will further protect your browsing experience, and that is the **uBlock Origin** add-on which is going to automatically block ads, pop-ups and trackers by default.

To install this add-on, in Firefox type this in the search bar: `about:addons`, then search for **uBlock Origin** and add it to your browser. By default, it will block a lot of nasty or annoying things, so unless you need to enable more advanced settings or filters/lists, you can just leave it as it is and move on.

## 🛠️ Task #8

Make sure **AppArmor** is installed and active. Quoting Ubuntu's website:

>[AppArmor](https://apparmor.net/) is an easy-to-use Linux Security Module implementation that restricts applications’ capabilities and permissions with **profiles** that are set per-program. It provides mandatory access control (MAC) to supplement the more traditional UNIX model of discretionary access control (DAC).

In Ubuntu 24.x AppArmor is installed and active by default, you can check its **status** using:

`aa-status`

or, for more details on profiles:

`sudo aa-status`

AppArmor profiles can be in either **Enforce** or **Complain** mode, where **Enforce** means that the policy defined in the profile will be enforced automatically, whilst **Complain** means that the policy will not be enforced but policy violations will be reported. By default, AppArmor configures some profiles in Enforce mode, whilst other may already be placed in Complain mode, or even unconfined. If you need to create or customize profiles for specific needs, check out the [documentation](https://ubuntu.com/server/docs/apparmor), otherwise stick with the defaults for now.

## 🛠️ Task #9

A best practice in Linux environments is **restricting or disallowing root logins**. However, always **make sure that you already have a user with administrative privileges** before blocking root access. For example, in the previous task if you managed to run the `sudo aa-status` successfully (with your current user's password), then your account has administrative privileges, meaning it's capable of using the `sudo` command to temporarily gain root privileges. Additionally, you can check to see if your username is included in the output of:

`getent group sudo`

If everything looks good, then to restrict root logins you should edit the `/etc/passwd` file. Use your preferred text editor, I like old-school vim. You can install vim on Ubuntu using:

`sudo apt install vim`

Here's a [guide to using vim](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-vim-101-a-beginners-guide-to-vim) if you're new to it.

Now, edit the **passwd** file using the command below. 

`sudo vim /etc/paswd`

On the first line, replace:

    root:x:0:0:root:/root:/bin/bash

with:

    root:x:0:0:root:/root:/sbin/nologin

Save and close the file.

Now, if you try the following commands, you should get "**This account is currently not available.**".

`sudo su`

`sudo -i`

## 🛠️ Task #10

Another best practice that you should implement on your **BASE** machine is **disabling unnecessary stuff**.

This is going to clean up and simplify your working environment, and will also **reduce your attack surface**.

* **Removing unnecessary apps**

Since I assume you performed **Task #1** already, you have chosen **Default Selection** during your fresh installation of Ubuntu. This already provided you with a clean and minimalistic OS. If you need to double-check for any useless apps, simply go to **Settings -> Apps** from your main menu and scroll through the list of installed apps. You probably don't need to remove anything if you followed the steps in **Task #1**.

* **Monitoring running services**

You can regularly **monitor the services actively running on your system** using the following commands:

`service --status-all`

`systemctl list-units`

* **Disabling Bluetooth**

You probably won't need Bluetooth, so why keep it enabled?

Go to **Settings -> Bluetooth** and disable it.

* **Disabling reporting**

To disable all kinds of **data collection** that Ubuntu may perform, use the following commands:

`ubuntu-report -f send no`

    sudo apt remove popularity-contest

Additionally, in your Ubuntu main menu go to **Settings -> Privacy & Security** and:
- Go to **Screen Lock** and turn on **Automatic Screen Lock**.
- Go to **Location** and disable **Automatic Device Location**.
- Go to **File History & Trash** and disable **File History**, then enable **Automatically Detele Trash Content** and **Automatically Delete Temporary Files**, set period to **1 day**.
- Go to **Diagnostics** and set **Send error reports to Canonical** to **Never**.

* **Disabling the camera and microphone**

Remember that **your BASE machine is completely separate from your personal machines and life**. Therefore, as an OSINT-er you won't ever need to show your face on camera or make voice calls. For this reason and your own protection, you should disable these services.

For disabling the **camera**, you need to edit the following file using your preferred editor:

`sudo vim /etc/modprobe.d/blacklist.conf`

Then, at the end of the file insert the following line:

`blacklist uvcvideo`

Next, open up a separate Terminal window to search for your **audio module** and type in:

    cat /proc/asound/modules

The result is going to be similar to: `0 snd_hda_dsp`

Now, in the same `/etc/modprobe.d/blacklist.conf` file where you blacklisted your camera, add another line at the end, and **make sure to replace the audio module name with your own**:

`blacklist snd_hda_dsp`

That's it. Save the file and close it.

**Note!** The blacklisting changes will be applied after **reboot**.

**Note!** Disabling the mic this way will also disable sounds on your **BASE** machine. If you ever need to listen to audio/video, you can remove the line from the file and then add it back again when you're done.

## 🛠️ Additional tasks

* Keep your Ubuntu up to date, regularly check for updates via **Settings -> System -> Software Updates**.
* **Do not ever login to any of your personal accounts** (email, social media, websites) on your **BASE** machine.
* **Do not download anything from the Internet**. You don't need to install 3rd party apps or download files on the **BASE**. Any OSINT-related apps or downloads are done only inside a dedicated VM.
* **Do not visit any shady websites** on your **BASE** machine's browser, even if you've performed all tasks above. No torrents, no dark web, no porn.
* **Do not plug in any USB or storage devices**, especially if you've plugged them already into other machines. You risk bringing malware or other unwanted stuff into your **BASE** machine.
* If you need secure storage to store files, use [ProtonDrive](https://proton.me/drive/download) (free version) which provides you with 5GB of encrypted storage.
* If you need email, go with [ProtonMail](https://proton.me/mail/download) (free) for one email address and 1GB storage space.
* **You don't really need an antivirus**. Linux viruses are quite rare and for this reason it's not worth having a 3rd party app sniffing everything you do.
* As an additional precaution, **cover your camera with black tape**. Best webcam protection ever.

## 🔍 What about the VMs?

Ok, so we covered the **BASE** machine which should be kept clean and secure at all times. 

On the other hand, **your OSINT work is going to be performed on dedicated VMs exclusively**. Since the VMs are running on top of your **BASE** machine, they will obviously "borrow" some of the security benefits of the tasks above, such as VPN traffic encryption, ufw protection, disabled camera and mic and so on.

However, on each VM you should implement some of the steps performed on the **BASE** machine in order to keep the VM clean and secure during your investigation. Your VM might be Ubuntu, Kali or another Linux distro of your choice. Just don't use Windows, ok?

So, **before starting any OSINT-related work**:

* Make sure the **VM's OS is updated**.
* Install **KeePassXC** for securley managing any data or logins locally on the VM.
* Repeat **tasks #6 and #7** for ensuring a safe browsing experience on the VM.
* Create and **use a separate email address** for that specific OSINT task only.
* Use the VM's storage space or a new ProtonDrive for your work on the VM.
* Keep in mind that the VM (OS, email, storage) must not interfere with **BASE**.
* Once your OSINT work is done, save your data if needed and **destroy the VM**.

## ⚠️ Final considerations

* I didn't mention **Tor**. In short, Tor might be blocked by various online services, and unless you need it for a specific task (e.g. browsing the dark web) I would prefer the hardened setup discussed above.
* I didn't mention **Tails**, which is an amnesic OS that you can run from a bootable USB drive with or without persistent storage. It may be a great choice for OSINT, but it comes with some limitations.
* I didn't mention **Qubes** or **Whonix**, which are highly-secured OSs aimed at more advanced users. Instead, I wanted to build a framework that almost anyone with some tech skills can implement.

## 🔄 OOO Framework updates

As they say, this is a living document. As various services and tools evolve, the framework will change accordingly. Also, if I decide to add or remove tasks or recommendations I will do so at my own discretion.

## 📜 Disclaimer

* All the information in this framework is intended to **protect yourself, your devices, your data and your OSINT work** from the ever-changing landscape of online threats. 
* In the context of this framework, **OSINT refers to passive, non-intrusive open-source intelligence** tasks.
* Any illegal or unethical use of this information is **your** responsibility.
