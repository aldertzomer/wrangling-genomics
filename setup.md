---
layout: page
title: Setup
---

<br>
This workshop was designed by datacarpentry to be run on pre-imaged Amazon Web Services 
(AWS) instances. For information about how to
use the workshop materials, see the 
[setup instructions](https://www.datacarpentry.org/genomics-workshop/setup.html) on the main workshop page.

<br>
**At Utrecht University from 2024** we are using a preconfigured linux server (gemini.science.uu.nl) and have provided required files in 
- `HOME/data` and
- presentations will be shared using blackboard.

<br>
On your **personal machine** you require some software to open/edit files and connect to the gemini server:
- A spreadsheet program (Excel, [LibreOffice](https://www.libreoffice.org/) (free), or something similar)
- A terminal to connect a secure shell. On windows you can use [mobaXterm](https://mobaxterm.mobatek.net/), [putty](https://www.putty.org/), [gitbash](https://git-scm.com/downloads), or the powershell. Mac has its own terminal.
- A file transfer program using sftp; You can use [WinSCP](https://winscp.net/), [filezilla](https://filezilla-project.org/) or something similar. This is convenient to (re)organise your files oor edit scripts/files in a graphical interface.
- An advanced text/script editor might be helpfull. On windows [notepad++](https://notepad-plus-plus.org/) is commonly used. Or cross-platform [sublimetext](https://www.sublimetext.com/) or build-in editors.

<br>
**To connect to the UU gemini server:**
- Terminal: `ssh your_solisid@gemini.science.uu.nl`
  + Login using your solis credentials
  + Setting the (conda) environment command `course B-MBIMIGE`
- **S**ecure **F**ile **T**ransfer: `sftp gemini.science.uu.nl`

🟢 At first login you can be prompted for secure shell access (fingerprint). Just accept this after checking that the gemini.science.uu.nl URL is correct.

<br>
When you login gemini using the terminal and start the course conda environment you should see something similar to below:  

&nbsp;&nbsp;&nbsp; ![image](https://github.com/user-attachments/assets/3335aedc-6f22-4b20-93ce-0351f6c3f400)

When you connect using a file browser like WinSCP:  

&nbsp;&nbsp;&nbsp; ![image](https://github.com/user-attachments/assets/22971006-a5aa-42b2-a409-99c0c672e1c0)

From there you can also directly open/inspect and edit (script) files...  

&nbsp;&nbsp;&nbsp; ![image](https://github.com/user-attachments/assets/5653d067-a6ff-4388-b2b5-03641d41b86b)
