Download Link: https://assignmentchef.com/product/solved-cs3339-lab-6-firewall-intrusion-detection-systems
<br>
<h1>Introduction</h1>

<strong> </strong>In this lab students will explore the Snort Intrusion Detection Systems. The students will study Snort IDS, a signature based intrusion detection system used to detect network attacks. Snort can also be used as a simple packet logger. For the purpose of this lab the students will use snort as a packet sniffer and write their own IDS rules.







<h2>Software Requirements</h2>

All required files are packed and configured in the provided virtual machine image.




<ul>

 <li>VirtualBox <u>https://www.virtualbox.org/wiki/Downloads</u></li>

</ul>




<ul>

 <li>The Ubuntu 18.04 Long Term Support (LTS) Version <u>https://s2.smu.edu/~rtumac/cs3339/spring2020/Lab6/</u> <u>https://ubuntu.com/download/desktop</u></li>

</ul>




<ul>

 <li>Snort: A signature-based Intrusion Detection System <u>https://www.snort.org/#get-started</u></li>

</ul>







<em>                                                                                                                                                                          </em>1







<h1>Starting the Lab 9 Virtual Machine</h1>

In this lab, we use Ubuntu as our VM image. Select the VM named Ubuntu CS3339.







Login the Ubuntu image with username student, and password CS3339ubnt. Below is the screen snapshot after login.

<h1>Installing Snort into the Operating System</h1>

<strong> </strong>

In our Lab 6 Ubuntu VM image, the snort has been installed and setup for you. If you want to use your own version of the image, you need to install snort into the operating system. To install the latest version of the snort, you can follow the installation instruction from the snort website. Note that installation instructions are vary from OSes. The instruction below shows how to install snort from its source code on Linux.




You can find more information here: <u>https://www.snort.org/#get-started</u>

While you install the snort, your system may miss some libraries. You need to install the required libraries, too.

<h1>Configuring and Starting the Snort IDS</h1>

<strong> </strong>

After installing the Snort, we need to configure it. The configuration file of snort is stored at /etc/snort/snort.conf. The screenshot below shows the commands to configure the Snort. You need to switch to root to gain the permission to read the snort configurations file.







After configuring the Snort, you need to start the Snort. You can simply type the following command to start the service.




$ snort -c /etc/snort/snort.conf -l /var/log/snort/

<h1>Snort Rules</h1>

Snort is a signature-based IDS, and it defines rules to detect the intrusions. All rules of Snort are stored under /etc/snort/rules directory. The screenshot below shows the files that contain rules of Snort.










The screenshot below shows a rule in the /etc/snort/rules/web-misc.rules

<h1>Writing and Adding a Snort Rule</h1>

Next, we are going to add a simple snort rule. You should add your own rules at

/etc/snort/rules/local.rules. Add the following line into the local.rules file <strong>alert icmp any any -&gt; any any (msg:”ICMP Packet found”; sid:1000001; rev:1;) </strong>

Basically, this rule defines that an alert will be logged if an ICMP packet is found. The ICMP packet could be from any IP address and the rule ID is 1000001. Make sure to pick a SID greater 1000000 for your own rules. The screenshot below shows the contents of the local.rules file after adding the rule.







To make the rule become effective, you need to restart the snort service. To accomplish this you can run the following two commands to stop and restart snort respectively.




$ kill -9 $(pidof snort)

$ snort -c /etc/snort/snort.conf -l /var/log/snort/

<h1>Triggering an Alert for the New Rule</h1>

To trigger an alert for the new rule, you only need to send an ICMP message to the VM image where snort runs. First, you need to find the IP address of the VM by typing the following command.

$ ifconfig

For instance, the screenshot shows the execution result on my VM image, and the IP address is 192.168.56.102




Next, you can open a terminal in your host. If you host is a Windows OS, you can use one of the following two ways to open a terminal

<ol>

 <li>Press “Win-R,” type “cmd” and press “Enter” to open a Command Prompt session using just your keyboard.</li>

 <li>Click the “Start | Program Files | Accessories | Command Prompt” to open a Command Prompt session using just your mouse.</li>

</ol>




After you have a terminal, you can just type the following command to send ping messages to the VM.

$ ping 192.168.56.102

After you send the ping messages, the alerts should be triggered, and you can find the log messages in /var/log/snort/alert. The screenshot below shows the result of reading the snort alerts.







You can see that the SID is 1000001, and the alerts are generated by the ICMP messages.

<h1>Assignments for Lab 6</h1>

<ol>

 <li>Read the lab instructions above and finish all the tasks.</li>

 <li>Answer the following questions and justify your answers. Simple yes or no answer will not get any credits.

  <ol>

   <li>What is a zero-day attack?</li>

   <li>Can Snort catch zero-day network attacks? If not, why not? If yes, how?</li>

  </ol></li>

</ol>




<ol start="3">

 <li>Write and add another snort rule and show me you trigger it.

  <ol>

   <li>The rule you added (from the rules file)</li>

   <li>A description of how you triggered the alert</li>

   <li>The alert itself from the log file</li>

  </ol></li>

</ol>







<strong>Happy Hacking!</strong>