<h1>Active Directory Lab: Remote Desktop Setup for Non-Administrative Users</h1>

<h2>Project Summary</h2>
<p>
  In this lab, I configure Remote Desktop access on Client-1 for non-administrative (normal) users.
  First, I modify the Remote Desktop settings on Client-1 to allow all Domain Users to connect.
  Then, from DC-1 I create a large batch of new user accounts using a PowerShell script.
  Finally, I verify that one of these newly created users can successfully log into Client-1.
</p>

<ul>
  <li><strong>Key Components:</strong>
    <ul>
      <li>Client-1 (Windows 10 Pro)</li>
      <li>DC-1 (Windows Server 2022 Datacenter)</li>
      <li>Remote Desktop configuration</li>
      <li>PowerShell user creation script</li>
    </ul>
  </li>
  <li><strong>Goal:</strong>
    Enable non-administrative remote access on Client-1 and validate user logins using bulk-created domain accounts.
  </li>
</ul>

<hr />

<h2>Steps &amp; Screenshots</h2>
<ol>
  <li>
    <strong>Configure Remote Desktop Access on Client-1</strong>
    <ol type="a">
      <li>
        Log into Client-1 as the Domain Admin (<code>mydomain.com\jane_admin</code>).
      </li>
      <p align="center">
        <img src="https://i.imgur.com/BKxrVuT.png" alt="Logging into Client-1 as jane_admin" width="600" />
        <br /><em>Figure 3.1 – Logging into Client-1 as jane_admin.</em>
      </p>
      <li>
        Open the Start Menu and navigate to <strong>Settings &gt; System &gt; Remote Desktop</strong>.
      </li>
      <li>
        Scroll down to the <strong>User Accounts</strong> section and click on <em>Select users that can remotely access this PC</em>.
      </li>
      <p align="center">
        <img src="https://i.imgur.com/EuENIzV.png" alt="Remote Desktop settings on Client-1" width="600" />
        <br /><em>Figure 3.2 – Navigating to Remote Desktop settings on Client-1.</em>
      </p>
      <li>
        In the Remote Desktop Users window, click <strong>Add</strong>, type <code>domain users</code>, check the entry, and add it so all domain users have remote access.
      </li>
      <p align="center">
        <img src="https://i.imgur.com/mIF3hNH.png" alt="Adding 'domain users' for Remote Desktop access" width="600" />
        <br /><em>Figure 3.3 – Adding 'domain users' to the Remote Desktop Users list.</em>
      </p>
    </ol>
  </li>
  <br />

  <li>
    <strong>Create Bulk User Accounts via PowerShell on DC-1</strong>
    <ol type="a">
      <li>
        Log into DC-1 as the Domain Admin (<code>mydomain.com\jane_admin</code>).
      </li>
      <li>
        Open Windows PowerShell (or ISE) as an Administrator.
      </li>
      <p align="center">
        <img src="https://i.imgur.com/VulnzZT.png" alt="Opening PowerShell on DC-1" width="600" />
        <br /><em>Figure 3.4 – Running PowerShell as an admin on DC-1.</em>
      </p>
      <li>
        Create a new file called <code>create-users.ps1</code> and copy the raw GitHub script into it. This script will generate a large number of user accounts.
      </li>
      <p align="center">
      <img src="https://i.imgur.com/Hy1v8N6.png" alt="github repo" width="600" />
      <img src="https://i.imgur.com/PLC9MiJ.png" alt="powershell and user script" width="600" />
      </p>
      <li>
        Save and run the script. The script will create 10,000 user accounts (all with the password <code>Password1</code>). Verify in Active Directory Users and Computers that new accounts are added under the <code>_EMPLOYEES</code> OU.
      </li>
      <p align="center">
        <img src="https://i.imgur.com/DfKOxPD.png" alt="New users created in ADUC" width="600" />
        <br /><em>Figure 3.5 – Active Directory Users and Computers showing newly created accounts.</em>
      </p>
    </ol>
  </li>
  <br />

  <li>
    <strong>Test Remote Desktop Login with a Newly Created User</strong>
    <ol type="a">
      <li>
        Log out of Client-1 (currently logged in as jane_admin).
      </li>
      <li>
        Log into Client-1 using one of the new user accounts (for example, <code>mydomain.com\kid.koxi</code>).
      </li>
      <p align="center">
        <img src="https://i.imgur.com/7cFfayQ.png" alt="Logging into Client-1 as kid.koxi" width="600" />
        <img src="https://i.imgur.com/ehojHUB.png" alt="Logging into Client-1 as kid.koxi" width="600" />
        <br /><em>Figure 3.6 – Logging into Client-1 with a non-administrative user account.</em>
      </p>
      <li>
        Once logged in, open Command Prompt (or PowerShell) and run <code>whoami</code> to confirm that you are logged in as the correct user.
      </li>
      <p align="center">
        <img src="https://i.imgur.com/lEXdNSa.png" alt="Verifying user identity via command prompt" width="600" />
        <br /><em>Figure 3.7 – Verifying the logged-in user identity on Client-1.</em>
      </p>
    </ol>
  </li>
</ol>

<hr />

<h2>Conclusion</h2>
<p>
  In this lab, I successfully configured Client-1 to allow remote desktop access for non-administrative users by adding the <code>domain users</code> group.
  Additionally, using a PowerShell script on DC-1, I bulk-created new user accounts and verified that one of these users could log into Client-1.
  This configuration enables a realistic user environment and prepares the system for further Active Directory management tasks.
</p>
