<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align = "center">osTicket - Prerequisites and Installation</h1> 
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines)</li>
  <li>Remote Desktop</li>
  <li>Internet Information Services (IIS)</li>
</ul>

</br>

<h2>Operating Systems Used </h2>
<ul>
  <li>Windows 10 (21H2)</li>
</ul>

</br>

<h2>List of Prerequisites</h2>
<ol>
  <li>Set up an Azure Virtual Machine (VM) environment (Windows 10 4 vCPUs Recommended)</li>
  <li><a href = "https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">osTicket Installation Files</a> (Download these files on your Azure Virtual Machine) </li>
  <li>Enable IIS in I.S.S.</li>
  <li>Install Web Platform Installer</li>
  <li>Install MySQL and set up username and password</li>
    <ul>
    <li>For this tutorial, we will set up our username and password as such:</li>
      <ul>
      <li>username: root</li>
      <li>password: Password1</li>
      </ul>
    </ul>
  <li>Install C++ Redistributable</li>
  <li>Configure permissions and install osTicket</li>
  <li>(OPTIONAL) Have a notepad on standby to keep track of usernames and passwords for this tutorial</li>
</ol>

<h2>Installation Steps</h2>

<h3>Install / Enable IIS in Windows WITH CGI and Common HTTP Features</h3>

<p>
  <ul>
    <li>In your VM, go to the <b>Control Panel</b> and head to <b>Programs</b>. </li>
    <li>Under <b>Program and Features</b> click on <b>Turn Windows features on or off</b></li>
    <li>Navigate the list and check the box for <b>Internet Information Services</b></li>
    <li>Expand the list for <b>Internet Information Services</b>, navigate to <b>World Wide Web Services</b> then expand that to find <b>Application Development Features</b>, expand that and check the box for <b>CGI</b>.</li>
    <li>Before closing, make sure the boxes under <b>Common HTTP Features</b> in World Wide Web Services are checked.</li>
      <ul>
        <li><b>Check these boxes in Turn Windows Features on or off</b></li>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/cd77ec6f-12af-4bb6-8120-daebad40dc00" height="50%" width="50%"
      </ul>
    <li>To confirm everything is set accordingly, go to your browser in your VM and type in <b>127.0.0.1</b>, it should load the page to Internet Information Services</li>
      <ul>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/71217cf0-2e60-48f2-ae86-e58fb5f008de" height="50%" width="50%" alt="Disk Sanitization Steps"/></li>
      </ul>
  </ul>
</p>


<br />

<h3>Installing Files for osTicket</h3>

<p>
  <ul>
    <li><b>NOTE:</b> Depending on your VM CPU and Google Drive's virus scanning system, downloads will be rather <i>slow</i></li>
    <li>From the Installation Files, download <b>PHP Manager</b> (PHPManagerForIIS_V1.5.0.msi) and <b>Rewrite Module</b> (rewrite_amd64_en-US.msi) </li>
    <li>Create a Folder in your VM's C Drive and name it <b>PHP</b></li>
      <ul>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/19fce899-a521-40bc-b8af-e484e9371540" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>From the Installation Files, download the zip file <b>PHP 7.3.8</b> (php-7.3.8-nts-Win32-VC15-x86.zip) then unzip the contents into PHP folder we've made (C:\ PHP)</li>
      <ul>
        <li><b>NOTE:</b> If a warning sign appears in the downloading icon in your browser, it means the Microsoft Defender Smartscreen in your VM is preventing you from downloading the zip file. If this happens, navigate the file your downloads and click on <b>Keep</b></li>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/3603641f-c860-4177-9472-e81fda25694a" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>From the Installation Files, download and install <b>VC_redist.x86.exe</b></li>
    <li>From the Installation Files, download and install <b>MySQL 5.5.62</b> (mysql-5.5.62-win32.msi)</li>
      <ul>
        <li>After installing, launch the <b>Configuration Wizard</b></li>
        <li>Check <b>Install As Window Service</b>, for this tutorial our Service Name will stay as <b>MySQL</b></li>
        <li>Check <b>Modify Security Settings</b> and for this tutorial we'll set the password as <b>Password1</b></li>
      </ul>
  </ul>
</p>

<br />

<h3>Setting up IIS and PHP</h3>

<p>
  <ul>
    <li>Open <b>Internet Information Services (IIS) Manager</b> and run it as Administrator</li>
    <ul>
      <li><b>PHP Manager</b> and <b>URL Rewrite</b> should be found in our IIS Manager due to the PHP Manager and Rewrite Modules files we have downloaded initially </li>
      <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/b264f093-2267-4dd0-a451-d879e8bb0ea0" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Go to <b>PHP Manager</b> and click on <b>Register new PHP Version</b>, set the directory to the <b>php-cgi</b> file found in the PHP folder we've set in C Drive (C:\PHP)</li>
    <ul>
      <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/aee8797b-729c-400e-a316-a6f7a9be889f" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
    </ul>
    <li>Optional but Recommened: Refresh the IIS Manager Server by going to <b>Actions</b> and under <b>Manage Server</b> click on <b>Restart</b></li>
  </ul>
</p>

<br />

<h3>Installing osTicket</h3>

<p>
  <ul>
    <li>From the Installation Files, download and install <b>osTicket v1.15.8.zip</b></li>
    <li>Extract the <b>upload</b> folder from the zip file and copy the folder into the directory <b>C:\inetpub\wwwroot</b> in your VM</li>
    <li>Rename the upload folder we've copied into wwwroot to <b>osTicket</b>, then reload IIS Manager</li>
    <li>In IIS Manager, expand the connection <b>Sites</b> then <b>Default Web Site</b> to click and highlight <b>osTicket</b>. Then, navigate to <b>Browse Folder</b> and click on <b>Browser*.80 (http)</b></li>
    <li>The page for osTicket Installer should now pop up, if it does not, check your directories of your files and folders</li>
      <ul>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/a15af79e-104b-4902-9c3d-c5c1062d475e" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>In IIS Manager, go to <b>osTicket</b> and click on <b>PHP Manager</b> and click on <b>Enable or disable extensions</b> and enable the following extensions</li>
      <ul>
        <li>php_imap.dll</li>
        <li>php_intl.dll</li>
        <li>php_opcache.dll</li>
      </ul>
    <li>Refresh osTicket Installer on your browser to see <b>PHP IMAP Extension</b> and <b>Intl Extensions</b> are checked signifying the extensions are installed</li>
    <li>After configurations locate the php file <b>ost-sampleconfig.php</b> inside the directory <b>C:\inetpub\wwwroot\osTicket\include\</b> and rename it to <b>ost-config.php</b> because osTicket Installer needs to interact with this file</li>
    <li>Now go to the <b>Properties</b> of the ost-config file and go to the <b>Advanced</b> settings in <b>Security</b> and <b>Disable Inheritance</b> to remove all inheritance permissions from the file (essentially making a "clean" object)</li>
    <li>Now add a new Permission, then click on <b>Select a principal</b> and for a new object type "everyone" the click on <b>Check Names</b> to set the Group and click OK. Then check all the boxes on Basic Permissions and then click OK. Now everyone using osTicket should have full permission to use it</li>
    <li>Head to osTicket on your browser and click on <b>Continue</b> then set your <b>System Settings</b> and <b>Admin User</b> until you get to <b>Database Settings</b></li>
      <ul>
        <li>For login information, you can set it to a fake email such as "yourname@helper.com", again it is recommended to have a notepad to keep your usernames and passwords on the standby</li>
      </ul>
    <li>From the Installation Files, download and install <b>HeidiSQL</b></li>
      <ul>
        <li>Go through basic setup then launch HeidiSQL and create a New Session using the username "root" and password "Password1"</li>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/bc6539b2-fbad-4962-8e25-7f843b7ad79d" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
        <li>You should see this once connected</li>
        <li><img src="https://github.com/Kasen-Elliot/osticket-prereqs-/assets/127895952/769ebd72-878f-4205-81e9-0d6e714a7141" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
        <li>Create a Database and name it <b>osTicket</b></li>
      </ul>
    <li>Once connected, go back to osTicket Installer type in our username and password into the respected fields in Database Settings</li>
      <ul>
        <li>MySQL Database: osTicket</li>
        <li>MySQL Username: root</li> 
        <li>MySQL Password: Password1</li>
      </ul>
    <li>Click <b>Install Now</b>, osTicket should now be fully installed on your VM!</li>
    <ul>
  
