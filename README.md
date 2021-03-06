
# IBM Digital Business Automation Exercise
## How to build a bot using WDG Automation RPA (Robotic Process Automation)

### Introduction
July 8th, 2020 IBM announced that it will be acquiring WDG Automation to strengthen IBM DBA portfolio (https://newsroom.ibm.com/2020-07-08-IBM-to-Acquire-WDG-Automation-to-Advance-AI-Infused-Automation-Capabilities-for-Enterprises). IBM has been in strategic co-operation with Automation Anywhere (AA), providing IBM RPA with Automation Anywhere RPA solution based on Automation Anywhere RPA platform. Although the co-operation with AA will continue, WDG Automation technology will join the IBM Cloud Integration organization and be available through IBM Cloud Pak for Automation on-premises, and in public or private cloud environments.

This exercise is a copy of current "Build a Bot Tutorial" available in IBM Demos (https://www.ibm.com/cloud/garage/dte/tutorial/build-bot-tutorial) that was originally built for IBM RPA with Automation Anywhere.

### Use case
In this exercise you will build a robot to automate processing of sales leads that arrive in a CSV/Excel format. Each row of the file represents a separate sales lead. The sales leads need to be manually entered (copy/paste) by an analyst into the online opportunity system of record (JK Automation Sales Leads). This task is error prone and the analysts repeatedly ask if this can be automated, but it has never been a company priority. Until now 😉

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

\
**(2) Create a new automation file (WAL file, WDG Automation Language)**
- Create a new WAL file by clicking the `New` icon from the top toolbar or `New` under "Get Started" section

  ![](./images/new.JPG)

- Select `WAL file` and click `Open`.

  ![](./images/open-new.JPG)

\
**(3) Create your bot script - Login to JK Automation website**

- You should now have your Studio opened with an empty WAL file in your Designer view. Note that you can change your view between _Script_, _Designer_ and _Call Graph_.

  ![](./images/empty-editor.JPG)

- Add `Start Browser` command from your Toolbox to your Designer view. You can find the command under _**Browser**_ --> _**Actions**_. Drag and drop it to your canvas.

  ![](./images/start-browser.JPG)

- The command configuration opens. You need to set name to your browser instance (for example `web01`). Keep `Google Chrome` selected as your browser type, if you have Chrome installed. You can also change the browser to one you want to use. Click `Save` button.

  ![](./images/config-start-browser.JPG)

- `Close Browser` configuration window pops up automatically. Make sure to set the same instance name value that you used for `Start Browser`. Also set `Keep browser open` as enabled. This helps you during the implementation so that browser is not closed when you test your automation and you can continue using it for defining next actions for your automation. Click `Save` button to close the configuration window.

  ![](./images/close-browser.JPG)

- Next command we want to is `Navigate`. You can find it also under _Browser_ --> _Actions_. Drag and drop it below the `Start Browser` command to your Designer view. Set the URL to **http://jk-automation.mybluemix.net** and click the `Save` button.

  ![](./images/navigate.JPG)

- **Save** your work by hitting `Ctrl+S` or the `Save icon` from the top toolbar. Name your automation WAL file to **jk-automation**. Your automation should now look as follows.

  ![](./images/1stsave.JPG)

- **Run** your automation to test that it works and JK Automation website is opened. Click the green `Run` icon form the top toolbar. Alternatively you can hit `F5`.

  ![](./images/start-icon.JPG)

- You should see new Chrome Browser window opened and JK Automation login page opened. **Note!** For the first time this might take a couple of seconds. When you go back to your Studio window, you should see `Execution succeeded` text at the bottom left-hand side corner. _**Make sure to leave the browser window open!**_

  ![](./images/success.JPG)

- Nice! Your first run with WDG Automation 👍🏻Let's keep on going! Next we will need to automate the login to JK Automation website.

> Currently WDG does not offer any mechanism to automate the capturing of objects (like web form fields) that you want to use in your automation. For web pages this needs to be done manually using browser functionality to inspect the object and copy the selector for it. WDG supports several selectors for fields: id, name, css, xpath, id + name.

- Open JK Automation browser window that you should have open. **Right-click** the `Username` field and from the opened menu select `Inspect`.

  ![](./images/open-inspect.JPG)

- This open your browsers element inspector with the Username field element selected. **Right-click** the selected element, select `Copy` --> `Copy selector`. This will copy the CSS selector for the element to your clipboard.

  ![](./images/inspect-editor.jpg)

- Go back to your WDG Studio and add `Set Value to Field` (Browser --> Fields) command to your automation just under `Navigation` command. When the command configuration window opens set _Value_ to "**whatever**" (username you use does not matter), _Selector Type_ to **Css** and _Css_ to **the value from your clipboard** (the selector you copied from element inspector). Finally click `Save`.

  ![](./images/setvalue-username.JPG)

- Similarly add new `Set Value to Field` command below the previous for the `Password` field. Set _Value_ to **password10**.

  ![](./images/setvalue-password.JPG)

- Now, let's finish the login sequence by adding a command to click the `Submit` button in the JK Automation login page. We'll do that by adding command `Click on Web Page` after the Set Value to Field commands. _**Note**_ that you can use toolbox search field to find commands. To display all the commands related to clicking, type **click** to the search field.

  ![](./images/toolbox-click.JPG)

-  Get the selector for the Submit button from your browsers element inspector as you earlier did for the Username and Password fields.

  ![](./images/click-submit.JPG)

- Your automation should look like as follows. Nice, good job!

  ![](./images/2nd-check.JPG)

\
**(4) Test your automation and continue implementation - Read CSV**

- `Save your work`, `close your browser with JK Automation login page` and `run your current automation as you did earlier`. You should see your bot executing, opening the JK Automation web page and logging in with the information that you used to develop the login sequence. When your bot is finished, you should see the JK Automation welcome page.

  ![](./images/welcome-page.JPG)

- Since we want to handle _Leads_, add a `Click on Web Page` command to your automation to click the `Leads` link in the left-hand side menu. Yet again, use your browsers element inspector to get the needed selector for the Leads link.

  ![](./images/click-leads.JPG)

- Click the `Download file` link in the left-hand side menu to download the CSV file that we will use to read some new sales leads from and add them to JK Automation system. _**Save the file to your computer and take note of the folder you saved it to**_. You will need that later on.

- When you have downloaded the CSV file, click the `Leads` link to open the JK Automation Sales Leads view in your browser.

  ![](./images/sales-leads.JPG)

- Good. We can now read the CSV file. Use toolbox search to find `Read CSV File` command and add it after your last Click on Web Page command.

- When the command configuration window opens, use the `folder browse icon` to select the file you just downloaded from your file system, leave all the other selections as they are in default. There are three outputs for the command: _Data Table_ (holds the data), _Rows_ (number of rows in the data table) and _Columns_ (number of columns in the data table). We want to store these to variables.

  ![](./images/read-csv.JPG)

- First, **Click** the folder icon besides the Data Table field to open variable list (as shown in picture above). Next, click `Add new variable` icon and the `Define Variable` window opens.

  ![](./images/add-new-variable.JPG)

- Name the variable as **leads**. Notice that the variable type is automatically set to match the output type (Data Table). Click `Save`.

  ![](./images/leads-variable.JPG)

- Repeat the previous steps to create variables also for other outputs _Rows_ and _Columns_. Name them **row_count** and **column_count**, respectively. Your `Read CSV File` command configuration should now look as follows. Click `Save`.

  ![](./images/read-csv-complete.JPG)

\
**(5) Store row data to variables**

Now, we obviously want to iterate through all the rows within the data table and insert the data to JK Automation Sales Leads page. Let's focus first on getting a lead read from the data table. There's an quite handy command named `Map Table Row` to do this. Use your toolbox search to find the command and drag and drop it under the `Read CSV File` command in your Designer view.

- When the configuration window opens, select variable **leads** to `Data Table` and then create a new variable for `Row` called **row_iterator** (since we want a variable to iterate through the data table) and set the default value for it to **1**.

  ![](./images/row-iterator.JPG)

- Next we need to create mappings for the data table row. If you open the CVS file that we're using for the lab with Excel / Notepad, you can see that there's 12 data rows and also 12 different columns: **First Name**, **Last Name**, **Job Tile**, **Company**, **email**, **phone**, **Client Address**, **Client City**, **Client State**, **Client Zipcode**, **Area of Interest** and **Followup Requested**.

  ![](./images/data.JPG)

- Click `plus sign (+)` within your `Map Table Row` configuration window to add all the needed mappings for your row. Use the `Column Name` to identify the data for the mapping and create a new variable to hold the data. Map and and name the variables as follows.

  ![](./images/map-datarow.JPG)

- Good. Click `Save` to save and close the configuration. Now we need to insert the data to JK Automation Sales Leads page that you should still have open in your browser.

> If you have closed JK Automation web page, you can always run your current automation to get the JK Automation Sales Leads page opened and continue from there.

\
**(6) Set Sales Leads input fields**

As you already earlier did (when creating the login sequence), use consecutive `Set Value to Field` commands to insert data that we just extracted to JK Automation Sales Leads page and to it's matching fields. Let's go through the first mapping together.

  - Right-click the `First Name` input field in the web page, select `Inspect` --> `Copy` --> `Copy Selector`

  ![](./images/first-sl-field.jpg)

  - Add `Set Value to Field` command to your automation under `Map Table Row` command and configure using it your just copied selector and the extracted variable **first_name**. **_NOTE!_** Enable also `Simulate Human` option. Click `Save`.

  ![](./images/fn-configuration.JPG)

- Similarly, set all the input fields till `Are of Interest` and when you have 11 consecutive `Set Value to Field` commands in your automation.

> Note. You can use copy-paste in your Designer view to easily copy commands.

- Next, add `If` command (Under _Base_ --> _Flow Control_) to your automatio under the last `Set Value to Field` command. Configure it using the **followup** variable as follows.

  ![](./images/if-followup.JPG)

- Add `Click on Web Page` command between _If_ and _End If_. Configure it with using the selector for the **_Follow up_ check box** in the Sales Leads web page.

  ![](./images/click-cb.JPG)

- Finally, add `Click on Web Page` command under _End If_ to click the **Submit** button in the Sales Leads web page

- **Save** your work, **close your browser** showing the JK Automation web site and **run** your automation by hitting the `Run` icon in the top toolbar. You should see your automation executing and entering the first sales lead (Dave Wakeman) to the JK Automation Sales Leads page. Nice!

  ![](./images/dave.JPG)

\
**(7) Format / cleanup automation defining different sequences as routines**

WDG Studio allows you to define and group parts of your automation as sub-routines. This can be useful to group logic parts of your automation script and make your automation more easily understandable.

- In your WGD Studio Designer view, select (_Shift+Click_) **all commands** between _Map Table Row_ and _Close Browser_ (**NOTE!** Do **NOT** select _Map Table Row_ and _Close Browser_!), right-click one of the selected commands and select **Advanced** --> **Extract Routine**.

  ![](./images/extract-routine.jpg)

- Name your sub-routine as **InsertLeadData**. Click `Save`.

  ![](./images/sr-insert-lead-data.JPG)

- Studio will show the extracted sub-routine. You can close it and return to "main" automation by clicking the _close icon_ after the name of the sub-routine.

  ![](./images/close-sr.JPG)

- You can now see the extrated sub-routine in your "main" automation script.

  ![](./images/sr-in-main.JPG)

  > Variables in WDG Studio are global. This means that you do not need to map variables between your main automation script and its sub-routines.

\
**(8) Add loop to iterate through the data table and finish your automation**

We have our automation almost ready. One of thing we still need to do, is to add a looping structure to iterate through all the sales leads within the data table that we read from the CSV file. WDG automation studio offers several structures to do this. We will use a `While` loop and use the **row_count** variable to go through all the records.

- Select the `Map Table Row` and the `Run Subroutine` commands, **right-click** one of the selected commands, and select _**Advanced**_ --> _**Surround With**_ --> _**While**_.

  ![](./images/while.JPG)

- Configure the While command using the **row_count** and **row_iterator** variables as follows. Click `Save`.

  ![](./images/config-while.JPG)

- You will now see the While loop in your main automation script.

  ![](./images/while-in-main.JPG)

- Good job! But something is missing... Right! We need still need to make sure that we increase our **row_iterator** value for each iteration. **Right-click** the `Run Subroutine` inside the While loop and select **Go To Definition**.

  ![](./images/goto-definition.JPG)

- Add `Calculate Mathematical Expression` command (Base --> Numeric) as the last command of the sub-routine. Configure it as follows. We want to add +1 at the end of each iteration.

  ![](./images/add-1.JPG)

- You should now have the command added to your sub-routine.

  ![](./images/1-added.JPG)

- Close the sub-routine to go back to main automation script. **Save** your work.

  ![](./images/finished.JPG)

\
**(9) Test your automation and final configurations**

Now it's time to test your implementation. Close your current browser window showing the JK Automation web site and click green `Run icon` from the studio toolbar.

You should see the automation / bot executing and adding all the sales leads to the JK Automation web site. Since we have not yet implemented logout and our `Close Browser` command is to configured to left browser open for testing, the automation halts when it has added all 12 sales leads to the JK Automation Sales Leads page. If, and hopefully when, your automation completes as expected, make the following final additions to your automation script.

- Implement logout from the JK Automation site by adding two `Click on Web Page` commands at the end of your automation, just before the `Close Browser` command. First one to **click your username** on the right-hand side upper corner of the web page and the second one to **click the logout link** from the menu opened. Again, use your browser to inspect the elements you want to interact with and copy the selector for them. _**This time try using XPath selectors**_.

  ![](./images/click-username.JPG)

- When you're done, you should have two `Click on Web Page commands` at the end of your automation before the `Close Browser` command.

  ![](./images/logout.JPG)

- **Save** your work, **close** the browser with JK Automation web site and **run** your automation again. You should now see your automation executing as previously, but after adding all the sales leads to JK Automation Sales Leads page, it also logs out from the site.

> It's always good practice to clean up after running the actual automation. Logout from different resources used and close down also the applications.

- Finally, change your `Close Browser` command configuration so that it closes the browser.

  ![](./images/close-browser-end.JPG)

- Save your work and test your automation again.

**Well done! Congrats finishing the exercise! Hope you learned some of the basics on how to use WDG Automation Studio. Keep on automating 😊**

---
_Author: Jukka Juselius (jukka.juselius@fi.ibm.com)_
