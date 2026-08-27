<h1>Secure File Storage and Access Management for Project Teams</h1>

<h2>1. Introduction</h2>

<p>This project demonstrates the implementation of a secure file storage and access management system for project teams in a Linux environment.</p>

<p>The project focuses on controlling access to a shared project directory, managing user permissions, configuring command history limits, monitoring file and directory access through Linux auditing, and providing a web-based interface for viewing audit logs.</p>

<p>The implementation uses Linux user and group management, Access Control Lists (ACLs), file and directory permissions, the sticky bit, Bash history configuration, <code>auditd</code>, Apache2, and HTTP Basic Authentication.</p>

<p>The project follows a practical security workflow covering <strong>user and permission management, access control, activity logging, web-based reporting, and security verification</strong>.</p>


<h2>2. Objective</h2>

<p>The objective of this project is to implement a secure file storage and access management system that restricts unauthorized file modifications, maintains user-specific access controls, records access activity, and provides a web-based mechanism for reviewing security audit information.</p>

<p>The project focuses on:</p>

<ul>
  <li>Creating separate user groups for Project A and Project B.</li>
  <li>Creating and managing individual user accounts.</li>
  <li>Configuring directory permissions and ACLs.</li>
  <li>Restricting unauthorized users from modifying or deleting project files.</li>
  <li>Applying default ACLs and the sticky bit to the project directory.</li>
  <li>Configuring command history limits for different users.</li>
  <li>Enabling Linux audit logging for the project directory.</li>
  <li>Automating the collection of audit logs.</li>
  <li>Developing a web-based reporting interface using Apache2.</li>
  <li>Protecting the web-based audit report using authentication.</li>
  <li>Verifying access controls, command history settings, audit logging, and web reporting.</li>
</ul>


<h2>3. Lab Environment</h2>

<p>The project was implemented in a Kali Linux virtual machine environment.</p>

<h3>Operating Environment</h3>

<ul>
  <li><strong>Operating System:</strong> Kali Linux</li>
  <li><strong>Virtualization:</strong> VirtualBox</li>
  <li><strong>Project Directory:</strong> <code>/home/project</code></li>
</ul>

<h3>User Groups</h3>

<p>Two project groups were created:</p>

<pre>
Project A → proja
Project B → projb
</pre>

<h3>Project A Users</h3>

<pre>
pa1
pa2
pa3
pa4
pa5
</pre>

<h3>Project B Users</h3>

<pre>
pb1
pb2
pb3
</pre>

<p>The project documentation establishes separate groups and user accounts for the two project teams.</p>


<h2>4. Tools and Technologies</h2>

<p>The following Linux tools and technologies were used:</p>

<table>
  <thead>
    <tr>
      <th>Tool / Technology</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Kali Linux</td>
      <td>Implementation environment</td>
    </tr>
    <tr>
      <td>VirtualBox</td>
      <td>Virtual machine environment</td>
    </tr>
    <tr>
      <td>Linux Users &amp; Groups</td>
      <td>User and team management</td>
    </tr>
    <tr>
      <td>ACL</td>
      <td>Fine-grained access control</td>
    </tr>
    <tr>
      <td><code>chmod</code></td>
      <td>Directory permission management</td>
    </tr>
    <tr>
      <td><code>chown</code></td>
      <td>Group ownership management</td>
    </tr>
    <tr>
      <td>Sticky Bit</td>
      <td>Restricting file deletion</td>
    </tr>
    <tr>
      <td>Bash</td>
      <td>Shell and command-history configuration</td>
    </tr>
    <tr>
      <td><code>auditd</code></td>
      <td>File and directory activity auditing</td>
    </tr>
    <tr>
      <td><code>ausearch</code></td>
      <td>Searching audit events</td>
    </tr>
    <tr>
      <td>Apache2</td>
      <td>Web server</td>
    </tr>
    <tr>
      <td><code>.htaccess</code></td>
      <td>Web access control</td>
    </tr>
    <tr>
      <td><code>.htpasswd</code></td>
      <td>Web authentication</td>
    </tr>
    <tr>
      <td>Cron</td>
      <td>Automated audit-log collection</td>
    </tr>
    <tr>
      <td>HTML/Web Browser</td>
      <td>Viewing the audit report</td>
    </tr>
  </tbody>
</table>

<p>The documented implementation uses Linux group management, ACLs, Bash configuration, <code>auditd</code>, Apache2, cron, and HTTP Basic Authentication.</p>


<h2>5. Assessment Methodology</h2>

<p>The project was implemented through the following sequence:</p>

<ol>
  <li>Establish user accounts and project groups.</li>
  <li>Create and secure the shared project directory.</li>
  <li>Configure ownership and directory permissions.</li>
  <li>Apply ACLs and default ACLs.</li>
  <li>Configure the sticky bit.</li>
  <li>Configure individual user shell settings.</li>
  <li>Apply command history limits.</li>
  <li>Install and configure <code>auditd</code>.</li>
  <li>Create audit rules for the project directory.</li>
  <li>Enable and verify audit logging.</li>
  <li>Install and configure Apache2.</li>
  <li>Automate the transfer of audit logs.</li>
  <li>Configure authentication for the web-based report.</li>
  <li>Verify unauthorized file deletion attempts.</li>
  <li>Verify command history settings.</li>
  <li>Verify audit logging.</li>
  <li>Access the web-based audit report using authenticated access.</li>
</ol>

<p>This workflow follows the five major tasks documented in the project.</p>


<hr>

<h2>6. Project Workflow</h2>

<pre>
User &amp; Group Creation
        ↓
Project Directory Creation
        ↓
File &amp; Directory Permissions
        ↓
ACL Configuration
        ↓
Default ACL + Sticky Bit
        ↓
Command History Configuration
        ↓
Auditd Configuration
        ↓
Access Logging
        ↓
Apache2 Web Reporting
        ↓
Web Authentication
        ↓
Security Verification
</pre>

<p>The workflow combines access control, user management, auditing, automated log collection, and authenticated web reporting.</p>


<h2>7. Step 1 — Establish User Accounts and Permissions</h2>

<p>The first phase established separate groups and user accounts for the project teams.</p>

<p>Two groups were created:</p>

<pre>
sudo groupadd proja
sudo groupadd projb
</pre>

<p>Five users were created for Project A and three users for Project B. Each user was assigned to the corresponding project group.</p>

<p>The project directory was then created:</p>

<pre>
sudo mkdir /home/project
</pre>

<p>Group ownership and directory permissions were configured, followed by ACL configuration for the individual project users.</p>

<p>Default ACLs were also applied so that access-control settings could be inherited by newly created content.</p>

<p>The sticky bit was enabled on the project directory to further control file deletion behavior.</p>

<h3>Result</h3>

<p>A shared project directory was established with user-specific access controls and additional file-management restrictions.</p>


<h2>8. Step 2 — Apply Directory and File Permissions</h2>

<p>The second phase focused on shell configuration and command history management.</p>

<p>The default shell for the project users was configured as <code>/bin/bash</code>.</p>

<p>Different command-history limits were configured for different users.</p>

<h3>Senior Analysts</h3>

<p>The documentation configures <code>pa1</code> and <code>pa5</code> with:</p>

<pre>
HISTSIZE=10
</pre>

<h3>Other Users</h3>

<p>The remaining users were configured with:</p>

<pre>
HISTSIZE=50
</pre>

<p>This configuration was added to the respective users' <code>.bashrc</code> files.</p>

<h3>Result</h3>

<p>Different command-history retention limits were configured according to the project's user roles.</p>


<h2>9. Step 3 — Enable Access Logging</h2>

<p>The third phase introduced Linux auditing for the project directory.</p>

<p>The <code>auditd</code> package was installed:</p>

<pre>
sudo apt-get install auditd -y
</pre>

<p>An audit rule was created to monitor the <code>/home/project</code> directory for read, write, execute, and attribute-related activities.</p>

<p>The documented audit rule uses the key:</p>

<pre>
project_access
</pre>

<p>The <code>auditd</code> service was then started and enabled so that auditing would remain active.</p>

<p>The service status and audit configuration were subsequently checked, and the audit service was restarted after the configuration was saved.</p>

<h3>Audit Verification</h3>

<p>The project used <code>ausearch</code> with the audit key to retrieve events:</p>

<pre>
sudo ausearch -k project_access
</pre>

<p>This allowed the generated audit events to be reviewed.</p>

<h3>Result</h3>

<p>Audit logging was configured to monitor activity associated with the project directory.</p>


<h2>10. Step 4 — Develop Web-Based Reporting Interface</h2>

<p>The fourth phase created a web-based mechanism for viewing the collected audit information.</p>

<p>Apache2 was installed as the web server:</p>

<pre>
sudo apt-get install apache2
</pre>

<p>Audit results were redirected into a file under the Apache web directory:</p>

<pre>
/var/www/auditlog.txt
</pre>

<p>The project then used <code>crontab</code> to automate the collection of audit information at regular intervals.</p>

<p>Apache configuration was modified to permit the required directory settings.</p>

<p>A <code>.htaccess</code> file was configured to protect access to the web-based report using HTTP Basic Authentication.</p>

<p>The documented authentication configuration included:</p>

<pre>
AuthType Basic
AuthName "Restricted Access"
AuthUserFile /var/www/html/.htpasswd
Require valid-user
</pre>

<p>An authenticated administrator account was then created using <code>.htpasswd</code>.</p>

<p>Apache2 was finally started and enabled.</p>

<h3>Result</h3>

<p>A password-protected web interface was configured for viewing the collected audit information.</p>


<h2>11. Step 5 — Verify and Validate Configurations</h2>

<p>The final phase validated the security controls implemented throughout the project.</p>

<h3>File Access Verification</h3>

<p>The <code>pa1</code> user was used to create a file inside the project directory:</p>

<pre>
/home/project/testfile.txt
</pre>

<p>The <code>pa2</code> user then attempted to remove the file.</p>

<p>The purpose of this test was to verify that the configured permissions and ACL restrictions prevented unauthorized file deletion.</p>

<h3>Command History Verification</h3>

<p>The <code>pa1</code> senior analyst account was used to display the command history and verify the configured history limit.</p>

<h3>Audit Logging Verification</h3>

<p>The audit events were searched using:</p>

<pre>
sudo ausearch -k project_access
</pre>

<p>This verified that project-directory activity was being recorded by the audit system.</p>

<h3>Web Report Verification</h3>

<p>Finally, the web browser was used to access the audit report through the local Apache server.</p>

<p>Authentication credentials were entered to verify protected access to the audit report.</p>


<h2>12. Results and Findings</h2>

<p>The project successfully implemented multiple layers of Linux-based security controls.</p>

<h3>Access Control</h3>

<p>User groups, directory permissions, and ACLs were configured to control access to the shared project directory.</p>

<h3>File Protection</h3>

<p>The project tested whether one user could remove a file created by another user, validating the configured access restrictions.</p>

<h3>Command History</h3>

<p>Different history limits were configured for senior analysts and other project users.</p>

<h3>Security Auditing</h3>

<p><code>auditd</code> was configured to monitor access to the project directory using the <code>project_access</code> audit key.</p>

<h3>Web Reporting</h3>

<p>Audit information was made available through an Apache-based web interface protected by HTTP Basic Authentication.</p>


<h2>13. Remediation Verification</h2>

<p>The project verified the implemented controls through practical tests.</p>

<p>The file-access test demonstrated the restriction against unauthorized deletion by another project user.</p>

<p>The command-history test verified that the senior analyst account displayed the configured history.</p>

<p>The <code>ausearch</code> command was used to confirm that access activity was being captured by the audit system.</p>

<p>Finally, the Apache web interface was accessed using authentication to verify that the audit report was protected from unrestricted access.</p>

<p>These tests provided validation of the access-control, auditing, and reporting configurations implemented during the project.</p>


<h2>14. Screenshots:</h2>
Step 1: User and Group Configuration <br/>
<br>
<p align="center">
<!-- <p align="center"> -->
<img src="https://i.imgur.com/gFmRUnj.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/BuMijzO.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/VS3K5yU.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/G48ox7p.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/1O9WLFq.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/eW4974x.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/Tnj2BW1.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/8QlgWIV.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/0m85CV8.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
</p>
Step 2:  Apply directory and file permissions: 
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/MrDdXw1.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/ohVoNkO.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/0hs8CMo.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
</p>
Step 3: Enable access logging: 
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/enoGU1l.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/Fnmoh3t.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/3l1q4mE.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/IeylC5N.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
</p>
Step 4: Develop web-based reporting interface: 
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/1fBiELt.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/UcuFYne.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/7pZ0ALv.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/kupWCT2.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
</p>
Step 5: Verify and validate configurations: 
<br/>
<br>
<p align="center">
<img src="https://i.imgur.com/dMK4X3c.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/mjKB8Lf.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
<img src="https://i.imgur.com/QyM1cfU.png" height="80%" width="80%" alt="Secure-file-access-managent"/>
<br />
<br />
</p>
<h2>15. Key Learnings</h2>

<p>This project provided practical experience with Linux-based security and access management.</p>

<h3>Technical Learnings</h3>

<ul>
  <li>Creating and managing Linux users and groups.</li>
  <li>Assigning users to project-specific groups.</li>
  <li>Managing file and directory ownership.</li>
  <li>Configuring Linux permissions using <code>chmod</code>.</li>
  <li>Managing group ownership using <code>chown</code>.</li>
  <li>Implementing fine-grained permissions using ACLs.</li>
  <li>Using default ACLs for inherited permissions.</li>
  <li>Understanding the purpose of the sticky bit.</li>
  <li>Configuring Bash command-history limits.</li>
  <li>Installing and configuring <code>auditd</code>.</li>
  <li>Creating audit rules for a specific directory.</li>
  <li>Searching audit events using <code>ausearch</code>.</li>
  <li>Automating log collection using cron.</li>
  <li>Configuring Apache2 as a web server.</li>
  <li>Protecting web resources using <code>.htaccess</code>.</li>
  <li>Implementing HTTP Basic Authentication.</li>
  <li>Validating security configurations through practical testing.</li>
</ul>

<h3>Security Learning</h3>

<p>The project demonstrated the importance of combining multiple security controls rather than relying on a single permission mechanism.</p>

<p>The implementation combined <strong>access control, auditing, authentication, and verification</strong> to improve the security of shared project resources.</p>


<hr>

<h2>16. Conclusion</h2>

<p>This project demonstrated the implementation of a Linux-based secure file storage and access management system for project teams.</p>

<p>The implementation began with the creation of project-specific users and groups, followed by directory permissions, ACL configuration, default ACLs, and the sticky bit. Command-history limits were then configured for different user roles.</p>

<p>To improve monitoring, <code>auditd</code> was configured to record activity associated with the project directory. The collected audit information was subsequently made available through an Apache-based web interface protected by authentication.</p>

<p>Finally, the implemented controls were validated through file-access testing, command-history verification, audit-event searches, and authenticated access to the web-based report.</p>

<p>Overall, the project provided practical experience in <strong>Linux access control, permissions management, auditing, authentication, log monitoring, and security validation</strong>.</p>


<hr>

<h2>17. Disclaimer</h2>

<p>This project was implemented in a controlled laboratory environment for educational and cybersecurity learning purposes.</p>

<p>The configurations and techniques demonstrated in this repository should be applied only to systems and environments for which you have appropriate authorization.</p>

<p>Do not use security testing, access-control testing, auditing, or authentication techniques against unauthorized systems or data.</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
