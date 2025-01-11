
<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align="center">osTicket - Prerequisites and Installation</h1>
<p align="center">This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.</p>

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Internet Information Services (IIS)</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows 10 (21H2)</li>
</ul>

<h2>Installation Steps</h2>

<h3>Step 1: Set Up an Azure Virtual Machine</h3>
<ol>
  <li>Create an Azure Virtual Machine with the following details:
    <ul>
      <li><strong>OS:</strong> Windows 10</li>
      <li><strong>4 vCPUs</strong></li>
      <li><strong>Name:</strong> osticket-vm</li>
      <li><strong>Username:</strong> Mateo123</li>
      <li><strong>Password:</strong> Password1!</li>
    </ul>
  </li>
  <li>Log in to the VM using Remote Desktop.</li>
</ol>

  <img src="https://i.imgur.com/o8pfoGa.png" alt="osTicket logo"/>
<h3>Step 2: Prepare osTicket Installation Files</h3>
<ol>
  <li>Inside the VM, download <strong>osTicket-Installation-Files.zip</strong> and extract it to your desktop.</li>
  <li>The folder should now be named <strong>osTicket-Installation-Files</strong>.</li>
</ol>

<h3>Step 3: Enable IIS and CGI in Windows</h3>
<ol>
  <li>Go to <strong>Control Panel > Programs > Turn Windows Features On or Off</strong>.</li>
  <li>Under <strong>Internet Information Services</strong>, enable:
    <ul>
      <li><strong>World Wide Web Services > Application Development Features > [X] CGI</strong></li>
    </ul>
  </li>
</ol>

<h3>Step 4: Install Required Tools</h3>
<ol>
  <li>From the osTicket-Installation-Files folder, install:
    <ul>
      <li><strong>PHP Manager for IIS</strong>: Run <code>PHPManagerForIIS_V1.5.0.msi</code>.</li>
      <li><strong>Rewrite Module</strong>: Run <code>rewrite_amd64_en-US.msi</code>.</li>
    </ul>
  </li>
  <li>Set up PHP:
    <ul>
      <li>Create a directory: <code>C:\PHP</code>.</li>
      <li>Unzip <code>php-7.3.8-nts-Win32-VC15-x86.zip</code> (from the folder) into <code>C:\PHP</code>.</li>
    </ul>
  </li>
  <li>Install Visual C++ Redistributable: Run <code>VC_redist.x86.exe</code> from the folder.</li>
  <li>Install MySQL 5.5.62:
    <ul>
      <li>Run <code>mysql-5.5.62-win32.msi</code>.</li>
      <li>Choose <strong>Typical Setup</strong>.</li>
      <li>After installation, launch the Configuration Wizard:
        <ul>
          <li>Select <strong>Standard Configuration</strong>.</li>
          <li>Set <strong>Username:</strong> root, and <strong>Password:</strong> root.</li>
        </ul>
      </li>
    </ul>
  </li>
</ol>

<h3>Step 5: Configure IIS for PHP</h3>
<ol>
  <li>Open IIS Manager (as Admin).</li>
  <li>Register PHP in IIS:
    <ul>
      <li>In PHP Manager, set PHP to: <code>C:\PHP\php-cgi.exe</code>.</li>
    </ul>
  </li>
  <li>Reload IIS: Stop and Start the server in IIS Manager.</li>
</ol>

<h3>Step 6: Install osTicket</h3>
<ol>
  <li>Unzip <code>osTicket-v1.15.8.zip</code> from the folder.</li>
  <li>Copy the <code>upload</code> folder to <code>C:\inetpub\wwwroot</code>.</li>
  <li>Rename the <code>upload</code> folder to <code>osTicket</code>.</li>
  <li>Reload IIS again: Stop and Start the server.</li>
  <li>Open IIS Manager:
    <ul>
      <li>Navigate to <strong>Sites > Default > osTicket</strong>.</li>
      <li>On the right-hand side, click <strong>Browse *:80</strong> to open osTicket in your browser.</li>
    </ul>
  </li>
</ol>

<h3>Step 7: Enable Required PHP Extensions</h3>
<ol>
  <li>Go back to IIS Manager:
    <ul>
      <li>Navigate to <strong>Sites > Default > osTicket</strong>.</li>
      <li>Double-click PHP Manager.</li>
      <li>Select <strong>Enable or disable an extension</strong>.</li>
      <li>Enable:
        <ul>
          <li><code>php_imap.dll</code></li>
          <li><code>php_intl.dll</code></li>
          <li><code>php_opcache.dll</code></li>
        </ul>
      </li>
    </ul>
  </li>
  <li>Refresh the osTicket page in your browser to see the updated status.</li>
</ol>

<h3>Step 8: Configure osTicket</h3>
<ol>
  <li>Rename the config file:
    <ul>
      <li>From: <code>C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php</code></li>
      <li>To: <code>C:\inetpub\wwwroot\osTicket\include\ost-config.php</code>.</li>
    </ul>
  </li>
  <li>Set permissions for <code>ost-config.php</code>:
    <ul>
      <li>Disable inheritance and remove all existing permissions.</li>
      <li>Add a new permission: <strong>Everyone > Full Control</strong>.</li>
    </ul>
  </li>
  <li>Continue the osTicket setup in your browser:
    <ul>
      <li>Enter a <strong>Helpdesk Name</strong> and <strong>Default Email</strong> (used for customer communications).</li>
    </ul>
  </li>
</ol>

<h3>Step 9: Set Up the Database</h3>
<ol>
  <li>Install HeidiSQL from the osTicket-Installation-Files folder.</li>
  <li>Open HeidiSQL and create a new session with:
    <ul>
      <li><strong>Username:</strong> root</li>
      <li><strong>Password:</strong> root</li>
    </ul>
  </li>
  <li>Connect to the session and create a database named <code>osTicket</code>.</li>
  <li>Return to the osTicket browser setup:
    <ul>
      <li>Enter:
        <ul>
          <li><strong>MySQL Database:</strong> osTicket</li>
          <li><strong>MySQL Username:</strong> root</li>
          <li><strong>MySQL Password:</strong> root</li>
        </ul>
      </li>
      <li>Click <strong>Install Now!</strong></li>
    </ul>
  </li>
</ol>

<img src="https://i.imgur.com/drTZzIS.png" alt="osTicket logo"/>
    <li>Done!!!<strong> Thanks for your time! </strong></li>

  <img src="https://i.imgur.com/wPmhyH1.png" alt="osTicket logo"/>
      <li>Set permissions for <code>C:\inetpub\wwwroot\osTicket\include\ost-config.php</code> to <strong>Read-only</strong>.</li>
    </ul>
  </li>
</ol>
