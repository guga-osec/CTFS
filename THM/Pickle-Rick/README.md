# Pickle Rick - CTF 🥒🚩

## Introduction
In the first place I did the recon and info gathering, after that I explore the ports.
<br>
<br>
Tools used:
<ul>
    <li>nmap
    <li>dirb
    <li>curl
    <li>ssh
    <li>nc
</ul>


### Recon & Info_Gath
First of all, turned on the tryhackme vpn so I can do the challenge.<br>
The first tool I used was `nmap`👁️ to see the open ports that the target might have had.
<div align="center">
    <img src="images/nmap_image.jpg" alt="Nmap image">
</div>



<p align=center>
    <br>
    the command:<br>
    <h3 align=center><code>nmap -Pn -sV &lt;target&gt; </code></h3>
</p>
<br>
means the following sets:<br>
<ul>
<li>-Pn : Treat the host as active <br>
<li>-sV : See the versions of the services<br>
 </ul>
<br>
Then I just write in the Notpad the info, for example:

<pre>
    IP:10.130.176.224
    
    nmap:
        service : port - version
        ssh : 22 - OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
        http : 80 - Apache httpd 2.4.41 ((Ubuntu))

    OS: Linux; CPE: cpe:/o:linux:linux_kernel
</pre>
<br>
Then I see the http port and investigate the page with curl. I end up comming across a commentary the rick let:<br>
<h4 align=center>
    <code>&lt;!-- <br>Note to self, remember username!<br> Username: R1ckRul3s<br>--&gt;</code>
</h4>
<br>
and wrote it down in the notepad too.<br>
<pre>
    main page :
        - found commentary _ important:
            Username: R1ckRul3s
</pre>
<br>
Now I use dirb so I can see the paths the page has.<br>
In this case I Don't specify the wordlist because the common one is sufficient.<br>
<div align="center">
    <img src="images/dirb_image.jpg" alt="Dirb image">
</div>
<br>
It ended up giving me some interesting paths, and as you know, also noted it in the notepad.<br>

<pre>
    dirb:
        + http://10.130.176.224/assets/ - non interesting
        + http://10.130.176.224/robots.txt - interesting
        + http://10.130.176.224/index.html - interesting
        + http://10.130.176.224/server-status - non interesting
        + http://10.130.176.224/login.php - interesting
</pre>

I started opening and seeing every URL, the assets wasn't interesting, the robots.txt had something writed: `Wubbalubbadubdub`, also noted it, index.html was the main page, server-status was forbidden and the most interesting.. the login.php, an as the path say login page, I tried to use a sqli but it didn't work.<br>
<div align="center">
    <img src="images/login_page.jpg" alt="login page image">
</div>
<br>
I remembered of the notes, Username: R1ckRul3s and tried the Wubbalubbadubdub as the password, and well it worked.<br>
Now I had a command panel, I used ls to see the files<br>
<div align="center">
    <img src="images/command_panel_page.jpg" alt="command panel page image">
</div>
<br>

After seeing the files I tried to use `cat` to see the "Sup3rS3cretPickl3Ingred.txt" and the "clue.txt" but i couldn't, so i search other ways to see and txt file and tried: `grep . <file> ` , it basically search everything in the file and print it .<br>
Well, I did it in the "Sup3rS3cretPickl3Ingred.txt" and it gave me the first flag `mr. meeseek hair`.<br>
Also did it in the "clue.txt" and it showed me `Look around the file system for the other ingredient.`.<br>
But I really didn't want to use the command panel page so I did an reverse shell with Python<br>

...need to continue

