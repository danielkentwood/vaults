# VS Code set up remote environments
created:: 2022-05-09 14:29
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis #Aetna/data 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[Aetna]], [[VS Code]]
***



from [https://cvshealth.stackenterprise.co/articles/540](https://cvshealth.stackenterprise.co/articles/540)

In this article I will walk through why & how to set up the Microsoft Remote Connection in VS code. This article assumes you already have VS code installed.

**Why Microsoft Remote Connection?**

Many Data Scientists who currently use VS code may SSH into our edge nodes by using the SSHFS extension. However, the SSHFS extension does not allow for certain extensions to be used when developing in a remote environment.

That's where Microsoft Remote Connection comes into play, because it allows you to effortlessly develop in a remote environment and use any extension you would like.

**How to install Microsoft Remote Connection?**

1.  Open up VS Code

2.  Click the extensions tab on the left hand side (it should look like 3 building blocks with a fourth in the air)

3.  Search for "Remote Development" and **install** the Remote Development extension. This should include 3 separate extensions in one(Remote-WSL, Remote - Containers, Remote - SSH)

4.  Once installed, click on the "Remote-SSH" extension -> settings gear next to it -> extension settings

5.  Scroll down to the "Remote.SSH: Local Server Download" setting and make sure that it's set to "always"

6.  In the same extension settings that you were in for steps 4 & 5, search for where it says settings.json and open the JSON

7.  In the settings.json files add to the end the following lines making sure that you don't disturb the formatting of the JSON:

```
 {
		"remote.SSH.localServerDownload": "always",
		"remote.downloadExtensionsLocally": true

	}
```

8.  On the left side of VS Code you should have another button that looks like a desktop computer, toggle the remote explorer setting from containers to SSH targets, then click which should open the Microsoft remote connection.

9.  Click the "+" button to the right of the words "SSH Targets"

10.  Now you can SSH into your desired edge node and put your password in -> you should now see VScode being installed into the remote environment

11.  To install extensions into the remote environment, go back to Extensions panel. In the bottom half, you should see a cloud with a down arrow to install local extensions in remote. We recommend to install at least Jupyter, Pylance, Python into the remote environment

12.  Uninstall SSHFS if installed


# VS Code Setup
from https://github.aetna.com/analytics-org/abc-tech-repo/blob/master/analytics_computing_environment/local/vscode/vscode_setup.md
1.  Once requested, downloaded, and installed; open VS Code. On Mac you can download it using the "Self Service" app under the heading "Developer".

**Please Note**: At this time, you should check the version of VS Code that you're running. The version that you downloaded from the App Store may be a little behind which will interfere with step #9. If your version is less than version 1.60, then you should try calling the SPOC IT Help Line at 1-888-905-9500 and asking them to remotely connect to your machine with elevated priveleges so they can run an update (Help > Install Update).

2.  Click the "Extensions" icon on the menu on the left bar (or press Ctrl+Shift+X; on Mac Cmd+Shift+X) then search for and install the following extensions:

-   Remote-SSH
-   Remote Development
-   Indenticator
-   SQL Formatter
-   Hive SQL
-   Python
-   YAML
-   Python Docstring Generator
3.  Using `cmder`, `cmd`, or `powershell`, run the following command to create an ssh key making sure to use your own email address:

**Please Note**: When prompted, you should accept the default file location and avoid creating a passphrase. In other words, press Enter 3 times.

```
ssh-keygen -t rsa -b 4096 -C "your_email@aetna.com"
```

4.  Once your ssh key has been created, you'll need to add it to your edge node. In order to do this navigate to `C:/Users/A123456/.ssh` and look for the `id_rsa.pub` file. You can either right-click the file, open it with notepad, and copy the contents to the clipboard _or_ copy it from your `cmder` terminal using the following command:

```
cat ~/.ssh/id_rsa.pub
```

Once copied to your clipboard, connect to your edge node from a terminal (e.g., `cmder` or `putty`) and paste it to the end of the `~/.ssh/authorized_keys` file. You can create/open the file with the following command:

```
nano ~/.ssh/authorized_keys
```

**Please Note**: If you already have entries in the `~/.ssh/authorized_keys` file, make sure there is a line break before pasting the new entry.

5.  Navigate to your User directory (i.e., C:\Users\A123456) and create a file called `ssh_config` using Notepad. Copy and paste the following contents making sure to replace a123456 with your AID:

```
Host xhadrevrm2p.aetna.com
	User a123456
	HostName xhadrevrm2p.aetna.com
	IdentityFile C:/Users/A123456/.ssh/id_rsa

Host xhadrevrm4p.aetna.com
	User a123456
	HostName xhadrevrm4p.aetna.com
	IdentityFile C:/Users/A123456/.ssh/id_rsa

Host xhadrevrm5p.aetna.com
	User a123456
	HostName xhadrevrm5p.aetna.com
	IdentityFile C:/Users/A123456/.ssh/id_rsa

Host xhadrevrm7p.aetna.com
	User a123456
	HostName xhadrevrm7p.aetna.com
	IdentityFile C:/Users/A123456/.ssh/id_rsa

Host xhadrevrm16p.aetna.com
	User a123456
	HostName xhadrevrm16p.aetna.com
	IdentityFile C:/Users/A123456/.ssh/id_rsa
```

6.  Open `cmd` by pressing Windows+r and then type in 'cmd' and press Enter. Once the command prompt opens, paste this:

ssh-keygen -t rsa -b 2048

This will generate the SSH key. Press Enter at the following prompt to save the key in the default location (under your user directory as a folder named .ssh). You will then be prompted to enter a secure passphrase, but you can leave that blank. You should now have a id_rsa.pub file which contains your new public SSH key.

**Please Note**: If `cmd` is not working, you should also be able to run the command from `cmder` or `git bash`.

7.  Open settings by navigating to: File > Preferences > Settings (on Mac Cmd+Comma, the standard Preferences shortcut)

8.  Modify user settings.json by searching for the term 'json', clicking one of the 'Edit in settings.json' links, replacing what's there with the json below (making sure to replace variable content), saving the changes, and then closing the file. On a Mac, you can ignore or comment out the terminal.integrated... section and you'll also need to modify any Windows paths.
```
{
	"editor.rulers": [80],
	"window.zoomLevel": 2,
	"sql-formatter.uppercase": true,
	
	"terminal.integrated.profiles.windows": {
		"cmder": {
		"path": "C:\\WINDOWS\\System32\\cmd.exe",
		"args": ["/K", "C:\\Users\\A123456\\Desktop\\cmder\\vendor\\bin\\vscode_init.cmd"]
		}
	},
	"terminal.integrated.defaultProfile.windows": "cmder",
	
	"remote.SSH.showLoginTerminal": true,
	"remote.SSH.lockfilesInTmp": true,
	"remote.SSH.defaultForwardedPorts": [    
		{
			"localPort": 10001,
			"name": "default",
			"remotePort": 443
		}
	],
	"remote.SSH.remotePlatform": {
		"xhadrevrm2p.aetna.com": "linux",
		"xhadrevrm4p.aetna.com": "linux",
		"xhadrevrm5p.aetna.com": "linux",
		"xhadrevrm7p.aetna.com": "linux",
		"xhadrevrm16p.aetna.com": "linux"
	},
	"remote.downloadExtensionsLocally": true,
	"git.ignoreLegacyWarning": true,
	"remote.SSH.enableAgentForwarding": false,
	"remote.SSH.enableDynamicForwarding": false,
	"remote.SSH.localServerDownload": "always",
	"remote.SSH.configFile": "C:\\Users\\A123456\\ssh_config",
	"remote.SSH.path": "C:\\Users\\A123456\\Desktop\\cmder\\vendor\\git-for-windows\\usr\\bin\\ssh.exe",
	"python.defaultInterpreterPath": "/users/a123456/.conda/envs/boa/bin/python",
}
```

9.  Run a command from the integrated terminal.

> **Test:**
> 
> _Open a terminal by clicking 'Terminal' along the top bar, selecting 'New Terminal' (or hotkey using Ctrl+Shift+`; on Mac Ctrl+`), and then typing the following command into the terminal (making sure to replace variable content)._
> 
> ssh YOUR_AID@YOUR_EDGE_NODE
> 
> **Expected result:**
> 
> [![vscode_terminal](https://github.aetna.com/analytics-org/abc-tech-repo/raw/master/analytics_computing_environment/local/vscode/images/vscode_terminal.png)](https://github.aetna.com/analytics-org/abc-tech-repo/blob/master/analytics_computing_environment/local/vscode/images/vscode_terminal.png)

10.  Connect to a remote server and create a workspace with one of your Git repos.

> **Test:**
> 
> _Click on icon in the bottom left hand corner of the VS Code window (hint: it looks like this: ><). Select 'Connect to Host...' and then select the edge node that you wish to connect to. If it's your first time connecting, this may take a couple minutes. Once you're connected, you should be able to add your Git repos from your edge node home directory as workspaces by selecting File > Add Folder to Workspace._
> 
> **Expected result:**
> 
> [![vscode_remote](https://github.aetna.com/analytics-org/abc-tech-repo/raw/master/analytics_computing_environment/local/vscode/images/vscode_remote.png)](https://github.aetna.com/analytics-org/abc-tech-repo/blob/master/analytics_computing_environment/local/vscode/images/vscode_remote.png)
> 
> **Note:** _If you are still having difficulty, refer to Microsoft's more comprehensive [instructions](https://code.visualstudio.com/docs/editor/integrated-terminal)_.

11.  While developing remotely, you'll want to take advantage of extensions like Python, Python Docstring, etc. You can check to see if your local extensions installed correctly by clicking on the Extensions icon on the left-hand side of your IDE. Please note that all of your local extensions may not be compatible with the remote server.

[![vscode_terminal](https://github.aetna.com/analytics-org/abc-tech-repo/raw/master/analytics_computing_environment/local/vscode/images/vscode_extensions.png)](https://github.aetna.com/analytics-org/abc-tech-repo/blob/master/analytics_computing_environment/local/vscode/images/vscode_extensions.png)

If you do not see the extensions under the SSH connected server, first try closing the IDE, reopening it, and reconnecting to the remote server. If you _still_ do not see the extensions (possibly due to a bug), try either of the following methods:

-   Method #1
	
	-   Use an SCP client (e.g., WinSCP) to copy the contents from your local VS Code extensions directory (C:\Users\A123456.vscode\extensions) to the remote VS Code extensions directory (/users/a123456/.vscode-server/extensions). Make sure to replace YOUR ID.
-   Method #2
	
	-   If your VS Code version is less than version 1.60, then proceed
	-   Open VS Code and connect to the remote server (refer to step #8 above)
	-   Navigate: File > Preferences > Settings
	-   Under 'Application' there should be a 'Proxy' setting that will allow you to enter the address of a proxy server
		-   Enter: http://[AID]:[Password]@proxy:9119
		-   Replace [AID] with your AID
		-   Replace [Password] with your password. Please note that if your password contains special characters that you'll need to URL encode them. You can use [this online tool](https://www.urlencoder.org/) to determine what you'll need to enter in place of the special characters. DO NOT enter your full password into the online tool, only the special characters.
	
	[![settings](https://github.aetna.com/analytics-org/abc-tech-repo/raw/master/analytics_computing_environment/local/vscode/images/settings_proxy.png)](https://github.aetna.com/analytics-org/abc-tech-repo/blob/master/analytics_computing_environment/local/vscode/images/settings_proxy.png)
        
12.  Read about other [tips and tricks](https://code.visualstudio.com/docs/getstarted/tips-and-tricks).

# Dealing with issues
[https://github.aetna.com/analytics-org/abc-tech-repo/issues/17](https://github.aetna.com/analytics-org/abc-tech-repo/issues/17)

