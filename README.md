<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket - Prerequisites and Installation

I will deploy and configure osTicket in this home lab on an Azure Windows VM to demonstrate and refine my administrative and user management skills.

## Environments and Technologies Used

- **Microsoft Azure** (Virtual Machines/Compute)
- **Remote Desktop**
- **Internet Information Services (IIS)**

## Operating Systems Used 

- **Windows 10** (21H2)

## Installation Steps

### 1. Create an Azure Virtual Machine (Windows 10, 4 vCPUs)
- **Name:** osticket-vm
- **Username:** Jane_Doe
- **Password:** osTicketPassword1!

### 2. Log into the VM with Remote Desktop

### 3. Download and Unzip osTicket Files
- Download the osTicket-Installation-Files.zip and unzip it on your desktop. The folder should be called “osTicket-Installation-Files”.

### 4. Install / Enable IIS with CGI Support
- Go to **World Wide Web Services -> Application Development Features** and ensure **CGI** is selected.
  
![image](https://github.com/user-attachments/assets/c6b053c2-5700-4c4e-b2b7-2db3094b37c5)

- Confirming IIS is enabled.
  
![image](https://github.com/user-attachments/assets/c2594daa-0444-4d74-83d7-080d338460b9)




### 5. Install PHP Manager for IIS
- From the “osTicket-Installation-Files” folder, install **PHP Manager for IIS** (PHPManagerForIIS_V1.5.0.msi).

![image](https://github.com/user-attachments/assets/b92eaa4a-0dcb-469d-9147-f4dd2c43f7aa)

### 6. Install the Rewrite Module
- Install the **Rewrite Module** (rewrite_amd64_en-US.msi).
  
  ![image](https://github.com/user-attachments/assets/85abece6-580e-408c-80b7-a514feea24ca)


### 7. Set Up PHP Folder
- Create the directory **C:\PHP**.
- Unzip **PHP 7.3.8** (php-7.3.8-nts-Win32-VC15-x86.zip) into **C:\PHP**.

![image](https://github.com/user-attachments/assets/c58995fa-b7e7-4c7e-908d-d8a3fe09d4d1)



### 8. Install Required Software
- From the “osTicket-Installation-Files” folder, install **VC_redist.x86.exe** and **MySQL 5.5.62** (mysql-5.5.62-win32.msi).
  - Choose **Typical Setup** and launch the configuration wizard after installation.
  - Configure with:
    - **Username:** root
    - **Password:** root
  
  ![image](https://github.com/user-attachments/assets/bb456b09-3a14-44c4-962f-c2c58bf19015)


  ![image](https://github.com/user-attachments/assets/4670429f-5a09-4d06-80c8-652e09488b65)


### 9. Register PHP with IIS
- Open IIS as an admin.
- Register PHP from within IIS: **PHP Manager -> C:\PHP\php-cgi.exe**.
- Reload IIS by stopping and starting the server.
  
  ![image](https://github.com/user-attachments/assets/a0423af6-486f-4585-b822-60d49b961e9b)



### 10. Install osTicket v1.15.8
- From the “osTicket-Installation-Files” folder, unzip **osTicket-v1.15.8.zip** and copy the **upload** folder to **C:\inetpub\wwwroot**.
- Rename the folder to **osTicket** (Ensure there are no spaces in the name).
  
  ![image](https://github.com/user-attachments/assets/1995f716-ead8-46b6-9886-6652fab32fbd)


### 11. Enable PHP Extensions
- Go back to IIS -> **Sites -> Default -> osTicket**.
- Open **PHP Manager** and enable the following extensions:
  - **php_imap.dll**
  - **php_intl.dll**
  - **php_opcache.dll**

  Refresh the site in your browser.

  ![image](https://github.com/user-attachments/assets/68f7de09-c176-40fa-8bf3-2680e89b5b18)
  ![image](https://github.com/user-attachments/assets/604ae332-dfbc-4c90-8526-4f78e6e93fc4)


### 12. Rename `ost-sampleconfig.php` to `ost-config.php`
- Navigate to **C:\inetpub\wwwroot\osTicket\include** and rename **ost-sampleconfig.php** to **ost-config.php**.
  
  ![image](https://github.com/user-attachments/assets/d0c73f6e-5eb6-43d7-bc10-b5a931a6a5e5)

### 13. Set Permissions for `ost-config.php`
- Right-click on **ost-config.php**, disable inheritance, remove all permissions, and grant **Everyone** full control.
  
  ![image](https://github.com/user-attachments/assets/0b6dae00-7939-48b7-8195-da8f01e9aa42)
  ![image](https://github.com/user-attachments/assets/d1cba096-b86b-4014-a210-9994f2b738b7)

### 14. Continue osTicket Setup in the Browser
- Access the setup page via **http://localhost/osTicket/scp/login.php**.
- Fill in the required details:
  - **Name Helpdesk**
  - **Default email** (receives emails from customers)

  ![image](https://github.com/user-attachments/assets/cbc952f9-c638-4884-9aec-418cd252cbda)

### 15. Set Up the MySQL Database
- Open **HeidiSQL** and create a session using the username and password: **root/root**.
- Create a new database called **osTicket**.

  ![image](https://github.com/user-attachments/assets/75461acc-ed86-48f3-908c-7445d473c420)

### 16. Complete osTicket Setup
- In the browser, configure MySQL details:
  - **MySQL Database:** osTicket
  - **MySQL Username:** root
  - **MySQL Password:** root
- Click **Install Now!**.

  ![image](https://github.com/user-attachments/assets/e37438f7-9617-4072-9866-3e3a61030e76)
  ![image](https://github.com/user-attachments/assets/11ecc5ea-ff67-4870-9727-90e9902f2a80)

### 17. Access osTicket
- Once installed, access the help desk login page: **http://localhost/osTicket/scp/login.php**.

  ![image](https://github.com/user-attachments/assets/0a1204e0-dd8e-41b5-9f0b-f2e4cbe96d49)

- End User's osTicket URL: **http://localhost/osTicket/**.

  ![image](https://github.com/user-attachments/assets/dbe09db6-b0a5-44e2-b119-2611b7a46093)

## Takeaways and Key Skills Developed

In this project, I successfully installed and set up **osTicket** on an Azure Windows VM to practice both admin and user skills. I configured the VM with **Windows 10**, installed **IIS**, **PHP**, and **MySQL** to support osTicket, and learned how to install and configure essential dependencies like **PHP Manager** and the **Rewrite Module**. The process also involved setting up and configuring **PHP extensions**, managing permissions, and creating a MySQL database. This project improved my understanding of web-based application installation, PHP configuration, and database management while also helping me troubleshoot issues during installation and configuration. It also provided hands-on experience with **Azure VM** setup and managing **Windows IIS** servers.
