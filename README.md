
# IBM Digital Business Automation Exercise
## How to build a bot using WDG RPA (Robotic Process Automation)

### Introduction
July 8th, 2020 IBM announced that it will be acquiring WDG Automation to strengthen IBM DBA portfolio (https://newsroom.ibm.com/2020-07-08-IBM-to-Acquire-WDG-Automation-to-Advance-AI-Infused-Automation-Capabilities-for-Enterprises). IBM has been in strategic co-operation with Automation Anywhere (AA), providing IBM RPA with Automation Anywhere RPA solution based on Automation Anywhere RPA platform. Although the co-operation with AA will continue, WDG Automation technology will join the IBM Cloud Integration organization and be available through IBM Cloud Pak for Automation on-premises, and in public or private cloud environments.

This exercise is a copy of current "Build a Bot Tutorial" available in IBM Demos (https://www.ibm.com/cloud/garage/dte/tutorial/build-bot-tutorial) that was originally built for IBM RPA with Auttomation Anywhere.

### Use case
In this exercise you will build a robot to automate processing sales leads that arrive in a CSV/Excel format. Each row of the file represents a separate sales lead. The sales leads need to be manually entered (copy/paste) by an analyst into the online opportunity system of record (JK Automation Sales Leads). This task is error prone and the analysts repeatedly ask if this can be automated, but it has never been a company priority. Until now 😉

#### Content
- [Blue Demos Environment](#blue-demos-environment)
- [Virtual Assistant](#virtual-assistant)
- [Connecting Chatbot to Business Automation Workflow](#connecting-chatbot-to-ibm-business-automation-workflow)
- [Automation](#automation)
- [Putting it all together!](#putting-it-all-together)  

#### Prerequisites
- [IBM Cloud](https://cloud.ibm.com) Account
- Access to a virtual environment with [IBM RPA](https://www.ibm.com/automation/software/rpa) and [IBM BAW](https://www.ibm.com/products/business-automation-workflow) installed


## Blue Demos Environment
If you are running this exercise using yourself reserved IBM Blue Demos environment, you need to complete the _**LAB 0: Setting Up Your Environment**_. **NOTE!** If you are doing this exercise in a class room session with an instructor, you can skip this and go directly to LAB 1. Your instructor will provide separate instructions to access your virtual environment and some of the environment details that you need in LAB 2.
  - [LAB 0: Setting Up Your Environment](./BlueDemos)

## Virtual Assistant
In this part we create our **Virtual Assistant / Chatbot** by importing a B2B Banking _skill_ to our Watson Assistant service. We also take a look at how our chatbot has been constructed and we can also test it out.
 - [LAB 1: Cognitive Chatbot Basics](./1-Basics)

## Connecting Chatbot to IBM Business Automation Workflow
Here we connect our chatbot to our managed workflow, so that our chatbot can trigger a new managed workflow instance when done collecting information from the banks corporate customer. We will use **IBM Cloud Functions** (serverless computing services) _actions_ to achieve this.
  - [LAB 2: Integrating Watson Assistant with IBM Business Automation Workflow (BAW)](./2-Functions)

## Automation
For this part of the exercise you will be using a ``virtual environment``running on cloud that you access via your web browser. Your instructor will tell you how to access your environment.
- [LAB 3: Business Automation Workflow](./3-BAW)
- [LAB 4: Robotic Process Automation](./4-RPA)

## Putting it all together!
- [LAB 5: Our solution in action](./5-Final)

If you manage to finish the labs 1 to 4, you can test and run the hole solution together!

---
_Author: Jukka Juselius (jukka.juselius@fi.ibm.com)_

_Kudos: Matias Kovero and Sandra Calvo Martinez for helping with the first draft_
