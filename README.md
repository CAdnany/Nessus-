# Nessus - 


A key component of ensuring the security of computer systems and networks is conducting vulnerability assessments. These assessments are designed to identify vulnerabilities, weaknesses, and other security issues that could potentially be exploited by attackers to gain unauthorized access or cause harm to the system.

There are many vulnerability scanners out there. Nessus for example, is a widely used vulnerability scanner that is designed to help organizations identify and address potential security issues in their systems.

To help you better understand how vulnerability assessments work, I’ve put together this project guide to help you gain that practical experience (Shout out to Josh Madakor for the idea).

> **What you’ll need:**

- VMware Workstation
- Windows 10 Iso file
- Nessus Essentials (through a web browser)

And don’t worry, all of the tools needed for this lab are free.

> **Project Overview:**

We will use Nessus Essentials to perform vulnerability assessments on a virtual Windows 10 machine inside of VMware Workstation. We’ll be running a regular scan, a credentialed scan, and then testing the vulnerability of an old version of Google Chrome. By the end of this project, we’ll have a better understanding of how to use Nessus Essentials to identify vulnerabilities and maintain a secure network.

I won’t be providing a step-by-step guide on setting up VMware and uploading a Windows VM into it as these are basic procedures that can be easily found through YouTube videos. Similarly, setting up Nessus on your host machine is a straightforward process that does not require detailed guidance.

**Okay, with that out of the way, let’s get started with the project tasks:**

# **Task 1: Run a regular scan of the Windows 10 VM**

1. Turn on your Windows VM from within VMware Workstation and make sure that it is on a “bridged network” so that your host machine can communicate with it.

2. Test that you can ping your Windows VM from your host terminal.
![[Pasted image 20240120092049.png]]
If you’re seeing “request timed out” or can’t ping the Win VM, make sure that the Win 10 firewall is fully turned off.

![[Pasted image 20240120092114.png]]
Type in “firewall” after clicking on the Windows icon and then open “Windows Defender Firewall,” then go to “Turn Windows Defender Firewall on or off” and turn it off for both the Private and the Public Network.

3. Launch Nessus Essentials through your host machine’s browser and create a new scan by navigating to this link: [https://localhost:8834/](https://localhost:8834/)

4. Click on “New Scan”
![[Pasted image 20240120092140.png]]

5. Choose the type of scan. In this case, we’ll choose “Basic Network Scan.”
![[Pasted image 20240120092157.png]]

6. Specify the target of the scan by entering the IP address of the Windows 10 VM, give the scan a name (“Regular Scan”) and then click “save.”
![[Pasted image 20240120092218.png]]

7. Once you’re satisfied with the scan settings, click on the “Launch” button to start the scan.
![[Pasted image 20240120092234.png]]

8. Monitor the scan progress. Nessus will display the scan progress in real time, showing you the number of vulnerabilities detected and their severity.

9. View the scan results once it’s done by clicking on the scan name. The results will include a list of vulnerabilities detected, their severity, and recommendations on how to remediate them.
![[Pasted image 20240120092257.png]]

Regular scan results

# **Task 2: Run a Credentialed Scan**

1. Configure the Windows VM to accept a credentialed scan:

- Enable remote registry: click on the start icon and then type “services.msc” and hit “enter.”
- Go to “remote registry,” double-click on it, and then click on “startup type.” Select “automatic” and then “apply” and hit “okay.”
![[Pasted image 20240120092442.png]]

- Enable file and printer sharing through “Advanced sharing settings” (it might already be turned on).
![[Pasted image 20240120092458.png]]

- Go to “user account control” and set it to “never notify,” hit “okay.”

![[Pasted image 20240120092519.png]]

- Go to the “registry editor” and add a remote key by navigating to: Local Machine > Software >Microsoft > Windows > CurrentVersion > Policies > System
- Right-click anywhere on the screen, select “new” and create a “Dword” called “LocalAccountTokenFilterPolicy.”

![[Pasted image 20240120092545.png]]


- Then double-1click on the one you just created and set its value to “1.”
- Restart the VM.

2. Launch Nessus Essentials and create a new scan with the same target IP and call it “Credentialed scan.”

3. Provide the credentials required to access the system under the “Credentials tab” by clicking on “Windows” and then input the username and password for the Windows VM.

4. Keep the other default settings and click on “Save” and then “Launch” the scan. Note that this scan will take much longer.

5. Once the scan is complete, view the scan results by clicking on the scan name.

You will notice a big difference between the results of the regular scan and the credentialed scan, because the credentialed scan will be able to identify more vulnerabilities as it has access to the system and can scan files and applications that are not accessible during a regular scan.

![[Pasted image 20240120092609.png]]

Credentialed scan: It yielded 87 vulnerabilities (critical, high, medium) compared to the regular scan’s 1 vulnerability.

![[Pasted image 20240120092649.png]]

# **Task 3: Download an old version of a web browser and then re-run the scan**

1. Download an older version of Google Chrome or Firefox from a safe source and install it.
2. Launch Nessus Essentials and rerun the credentialed scan.
3. Click on the “Launch” button to start the scan.
4. Analyze the scan results once the scan is complete.

You will find that the scan has identified new vulnerabilities related to the older version of Google Chrome. This is because older versions of software are often more vulnerable to attacks, and attackers are more likely to target them.

![[Pasted image 20240120092708.png]]

The critical and high vulnerabilities have more than doubled in number


![[Pasted image 20240120092721.png]]

The outdated Chrome version is at the top of the list in vulnerabilities.

# **Task 4: Remediate the vulnerabilities and run another scan.**

1. Update Google Chrome to the latest version.
2. Run Windows Update to fix some of the other vulnerabilities.

![[Pasted image 20240120092742.png]]
3. Open Nessus Essentials and relaunch the previous “Credentialed Scan.”

4. Analyze the scan results.
![[Pasted image 20240120092757.png]]

Only one critical and high vulnerability remains after the updates.

You’ll now notice that the vulnerabilities related to the older version of Google Chrome are no longer present in the scan results. Other vulnerabilities have also been remediated with the Windows update. This is because updating to the latest version of software often includes security patches that address known vulnerabilities, which shows the importance of always updating your software. It makes our job a lot easier.

> **Lessons Learned from This Project**

In this project, we learned how to use Nessus Essentials to perform vulnerability assessments. We performed both regular and credentialed scans, and then we saw live how updating software can remove a lot of vulnerabilities.

# **Through these exercises, we gained the following skills and lessons:**

- Understanding the importance of vulnerability assessments in maintaining a secure network.
- Familiarity with Nessus Essentials and its capabilities in identifying vulnerabilities.
- Knowledge of how to configure and run both regular and credentialed scans.
- Understanding the vulnerability of older software versions and the importance of keeping software up-to-date.
- The ability to interpret and act on the scan results to improve the security of the system.

# **Next Steps and Building on this Project**

Now that you have completed this Nessus vulnerability scanning lab, there are several ways you can build on your skills and knowledge to improve your network security. Here are some recommendations for next steps:

1. Implement Remediation Plans: After identifying vulnerabilities through Nessus scans, it is essential to remediate them. You can create a remediation plan and implement it to address the vulnerabilities identified during the Nessus scan.

2. Customize Scan Settings: Nessus offers a high level of customization when it comes to scan settings. You can customize your scan settings to prioritize the vulnerabilities you want to address or exclude specific IPs or subnets from the scan.

3. Perform Regular Scans: To maintain the security of your network, it is important to perform regular Nessus scans. Consider setting up a schedule to perform regular scans, perhaps on a weekly or monthly basis.

4. Further Research: Nessus is a powerful tool that offers a wealth of information on network security. Consider researching and learning more about Nessus and other vulnerability scanning tools to enhance your knowledge and skills.

By implementing these next steps, you can continue to build on the skills and knowledge gained through this Nessus vulnerability scanning project, and ultimately improve the security of your network. I hope you enjoyed this short read and learned something new.

