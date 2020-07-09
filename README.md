
# IBM Digital Business Automation Exercise
## How to build a bot using WDG RPA (Robotic Process Automation)

### Introduction
July 8th, 2020 IBM announced that it will be acquiring WDG Automation to strengthen IBM DBA portfolio (https://newsroom.ibm.com/2020-07-08-IBM-to-Acquire-WDG-Automation-to-Advance-AI-Infused-Automation-Capabilities-for-Enterprises). IBM has been in strategic co-operation with Automation Anywhere (AA), providing IBM RPA with Automation Anywhere RPA solution based on Automation Anywhere RPA platform. Although the co-operation with AA will continue, WDG Automation technology will join the IBM Cloud Integration organization and be available through IBM Cloud Pak for Automation on-premises, and in public or private cloud environments.

This exercise is a copy of current "Build a Bot Tutorial" available in IBM Demos (https://www.ibm.com/cloud/garage/dte/tutorial/build-bot-tutorial) that was originally built for IBM RPA with Auttomation Anywhere.

### Use case
In this exercise you will build a robot to automate processing sales leads that arrive in a CSV/Excel format. Each row of the file represents a separate sales lead. The sales leads need to be manually entered (copy/paste) by an analyst into the online opportunity system of record (JK Automation Sales Leads). This task is error prone and the analysts repeatedly ask if this can be automated, but it has never been a company priority. Until now 😉

### Prerequisites
- Personal WDG Automation Account activated
- WDG Studio installed and configured to your computer

### Exercise instructions
**(1) Start WDG Automation Studio**
- Double-click the `WDG Studio shortcut` in your desktop.

![](./images/shortcut.JPG)

- When the login window opens (might take a while for the first time), type in your username and hit the `Login button`.

![](./images/login.JPG)

- When your tenant name is displayed, type in your password and hit the `Login button` again.

<!-- ![](./images/login2.JPG) -->

**(2) Create a new WAL file by clicking the `New` icon from the top toolbar or `New` under "Get Started" section**

![](./images/new.JPG)

- Select `WAL file` (WDG Automation Language) and click `Open`.

![](./images/open-new.JPG)

**(3) Create your bot script**

You should now have your Studio opened with a empty WAL file in your Designer view. Note that you change your view between Script, Designer and Call Graph.

![](./images/empty-editor.JPG)

- Add `Start Browser` command from your Toolbox to your Designer view. You can find the command under Browser --> Actions. Drag and drop it to your canvas.

![](./images/start-browser.JPG)

- The command configuration opens. You need to set name to your browser instance (for example `web01`). Keep `Google Chrome` selected as your browser type, if you have Chrome installed. You can also change the browser to one you want to use. Click `Save` button.

![](./images/config-start-browser.JPG)

- `Close Browser` configuration window pops up automatically. Make sure to set the same instance name value that you used for `Start Browser`. Also set `Keep browser open` as enabled. This helps you during the implementation so that browser is not closed when you test your automation and you can continue using it for defining next actions for your automation. Click `Save` button to close the configuration window.

![](./images/close-browser.JPG)

- Next command we want to is `Navigate`. You can find it also under Browser --> Actions. Drag and drop it below the `Start Browser` command to your Designer view. Set the URL to `http://jk-automation.mybluemix.net` and click the `Save` button.

![](./images/navigate.JPG)

- Save your work by hitting `Ctrl+S` or the `Save icon` from the top toolbar. Name your automation WAL file to `jk-automation.wal`. Your automation should now look as follows.

![](./images/1stsave.JPG)

- Run your automation to test that it works and JK Automation website is opened. Click the small arrow below green `Run` icon form the top toolbar and select `Run without debugging`. Alternatively you can hit `Ctrl+F5`.

![](./images/start-wo-debug.JPG)

- You should see new Chrome Browser window opened and JK Automation login page opened. Note! For the first time this might take a couple of seconds. When you go back to your Studio window, you should see `Execution succeeded` text at the bottom left-hand side corner. *_Make sure to leave the browser window open!_*

![](./images/success.JPG)

**(4) Test your automation**


---
_Author: Jukka Juselius (jukka.juselius@fi.ibm.com)_
