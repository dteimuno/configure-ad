<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
Setup Resources in Azure
</p>
<p>
1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”
<img width="796" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/d792d7bc-31a1-4011-930e-903d7f7416bc">

  a. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
<img width="793" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/672091be-2129-47b6-8c43-966d7d2fe08e">

2. Set Domain Controller’s NIC Private IP address to be static
<img width="1434" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/c9537949-4521-4b96-891e-df178294f0f1">

3. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a
   <img width="812" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/e5f9ea0e-ee43-4d4c-9ae9-b8a0788aad76">

4. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher
  <img width="849" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/0ff116f3-7bc8-4bdc-8bc2-139264166d63">

</p>
<br />
Ensure Connectivity between the client and Domain Controller
<p>
</p>
<p>
5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
  <img width="591" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/1d29f021-e658-4b9a-8e91-05d092472495">
<img width="974" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/f301a1aa-0a04-49a5-9d54-d05810bf0bc1">
<img width="975" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/096949e9-66e9-46da-9a48-4ef369331c79">

6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
   <img width="1436" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/873995f0-02b0-4b64-8bf7-51eea5b3bb8e">
<img width="947" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/7f453d93-2d3d-4a0a-83ec-7c214eac762d">
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/f5866fd0-274f-4e4c-a6c7-a321e363bc8a">

7. Check back at Client-1 to see the ping succeed
<img width="976" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/2fbcc49b-ea9f-46fe-a606-b36c11c5b4f0">

</p>
<br />

<p>
</p>
<p>
8.Login to DC-1 and install Active Directory Domain Services
<img width="1439" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/b3226e7a-fc28-4c26-a938-7d708b0f1b97">
<img width="785" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/f7c98cfa-394e-4d22-9271-0e075c6eefa4">
<img width="789" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/eafc3a93-fc07-4c35-95c6-7b97f39635de">
<img width="793" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/6c803809-8274-4baa-a561-9501ac47d00d">
<img width="789" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/42694a80-db79-4ab5-9cd6-93b1c24cc98a">
<img width="793" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/9f66591c-7bc4-4bad-8f2d-4c6f4f929b94">
<img width="794" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/05607c59-02f0-46da-a4e6-f873bde053ca">
<img width="794" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/aadc355e-c465-4a05-8255-cea67fe9f929">
<img width="790" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/16a97a50-ebce-4e16-b4a6-fe0d3d237684">
<img width="797" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/e4e9733c-ccd4-44c8-8ddd-75a6ff06a935">

9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/8522cb11-e493-4520-8fd9-2f46d4e0d5cc">
<img width="759" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/c7bd2b21-3bd4-4f79-b07e-4e37ab329966">
<img width="758" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/ca3f326f-ff19-419e-80d3-5112bbfd36a1">
<img width="753" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/af3f4024-ddcd-4752-9709-34f0ab52c547">
<img width="757" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/3c777641-ab57-48ae-b09c-0572e31019c4">
<img width="759" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/fd6b7513-4785-4ae5-b37b-de6a9c53a86e">
<img width="758" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/5ac664d2-f418-43eb-b9d0-96cf62e42825">


10. Restart and then log back into DC-1 as user: mydomain.com\labuser
<img width="665" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/145fad32-bb59-483e-966b-b01a2046c4e9">

</p>
<br />

<p>
</p>
<p>
  
11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
<img width="750" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/89bf95aa-3d0a-424a-9b90-b29cbf086ec1">

12. Create a new OU named “_ADMINS”
<img width="750" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/a29fb634-6562-434b-b0ff-ad4802aa48be">

15. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
    <img width="749" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/d21ba837-6980-4c1f-960a-6799ce00856f">
<img width="752" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/b0e4add4-9515-4305-a8ec-bc24674373ad">
<img width="750" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/a1939ab0-db21-4c47-8022-54ed25a4b9de">
<img width="750" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/78220f3e-48fb-49ac-9aa5-97c1291df237">

17. Add jane_admin to the “Domain Admins” Security Group
    <img width="751" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/faa2ed97-fb25-4868-8d23-ff7964b03fc1">
<img width="743" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/d29a6a6f-ff03-4d16-aa83-a13da4cdd235">

19. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
20. User jane_admin as your admin account from now on

</p>
<br />

<p>
</p>
<p>
17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
<img width="949" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/98f4847a-a7f6-4aed-8511-f49d5de69ae8">

18. From the Azure Portal, restart Client-1
  <img width="1435" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/821de44d-da8f-429f-a2b1-8d10fd559325">

19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
  <img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/072d3dd3-4722-48c8-b4cf-c1e92d0f0210">
<img width="1176" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/73a8227c-5221-40b3-a49c-417eeac6f9e7">
<img width="811" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/05812811-56fe-4bcd-a04c-58f784700e8f">
<img width="686" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/1519af5a-d19e-40e2-b968-f01314cd27e3">

20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
22. Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes. I guess I skipped this in the lab!)

</p>
<br />

<p>
</p>
<p>
22. Log into Client-1 as mydomain.com\jane_admin and open system properties
23. Click “Remote Desktop”
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/37bbb968-01be-4a35-b384-3c57b453ca66">

24. Allow “domain users” access to remote desktop
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/a4857ebb-7abc-418b-abe5-25822270eae3">
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/400f549f-61b1-4c14-a554-091ee8822789">

25. You can now log into Client-1 as a normal, non-administrative user now
27. Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)

</p>
<br />

<p>
</p>
<p>
27. Login to DC-1 as jane_admin
28. Open PowerShell_ise as an administrator
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/43a17388-0811-49c5-8720-d15f5748d75e">

29. Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
<img width="1281" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/d7501a98-8324-48a8-a855-5326cbd7c151">

30. Run the script and observe the accounts being created
<img width="1281" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/878241dd-2f95-4748-bf54-5fb3e042a1c5">
<img width="773" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/abd3ec92-aae2-493f-9b70-9739b4d1bc7b">

31. When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)
<img width="666" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/87b4a4c9-faf0-4923-826f-11b1e84cddb0">
<img width="1440" alt="image" src="https://github.com/dteimuno/configure-ad/assets/169619672/89dbaf44-bde2-48b9-9cae-80c14b4dd60d">

</p>
<br />
