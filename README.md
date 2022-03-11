# TryHackeMe-Web_Fundamentals-LFI


We are given an ip and questions in order to complete this room in TryHackMe, Web Fundamentals.

## Getting User Access via LFI


### **Look around the website. What is the name of the parameter you found on the website?**

If we visit the ip we are given, we are met with a home page: 

![image](https://user-images.githubusercontent.com/86057471/157699687-5f585827-1f8e-46ca-8752-13e394d594fb.png)

We need to try and find the parameter. We can try clicking on *About* to see what happens:

![about](https://user-images.githubusercontent.com/86057471/157700490-1e0db46c-7375-45ea-a1eb-4596d5a6c284.png)

The page hasn't changed but the url has changed: 

![about url](https://user-images.githubusercontent.com/86057471/157700571-e73ac9df-d96e-4a62-870a-cf320767fc75.png)

We can see that that the parameter is called **page**

### **What is the name of the user on the system?**

To find users on the system we can try to access the /etc/passwd file: 

![etc passwd](https://user-images.githubusercontent.com/86057471/157702776-48d6d0c3-cde8-4aaf-b059-22e287db6091.png)

Now we have accessed the /etc/passwd file. If we look through the file we find the username **falcon**

![home falcon](https://user-images.githubusercontent.com/86057471/157704807-2bb819d5-8055-4c98-8802-eb87b37e3fb1.png)

### **Name of the file which can give you access to falcon's account on the system?**

Knowing an account name, falcon, we can try and login using ssh. We don't have the password but we can use the ssh key to login, which can be found in **id_rsa**:

![id rsa](https://user-images.githubusercontent.com/86057471/157707162-79d2e5f0-d447-4c91-9f4a-34efef54d3d4.png)

### **What is the user flag?**

After getting the ssh key we need to copy it to a file and use it to login through ssh:

![falconsssh](https://user-images.githubusercontent.com/86057471/157708498-07f4c478-a154-42e9-85ec-11accf4014b5.png)

We then get the need to cat out the file user.txt.

![user txt](https://user-images.githubusercontent.com/86057471/157708930-afda6475-c470-4a55-b7db-e27d507057ee.png)

## Escalating Your Privileges to Root

### What can falcon run as root?

To find out what falcon can run as root we can check the sudo permissions by using "sudo -l":

![sudo -l](https://user-images.githubusercontent.com/86057471/157890779-91980c70-1c5e-437a-bf4a-6f5551f50e8b.png)

We see that falcon can run **/bin/journalctl** as root.

### What is the root flag?

After finding that falcon can run journalctl as root we can check gtfobins for any privilege escalations using journalctl.

![gtfobins](https://user-images.githubusercontent.com/86057471/157891366-d318ea95-a6e8-4aa0-aa2e-5b03b4d0f4c4.png)

In gtfobins there is a privilege escalation for journalctl. Since we run journalctl as sudo we will using the sudo option. All we need to do is copy and paste from journalctl to our terminal:

![root](https://user-images.githubusercontent.com/86057471/157892087-085ebd6b-3789-4a7d-8542-5bd0316bb1a0.png)

We are now root.

Now all we need to do is to find the root.txt which we can find in the root folder and cat it out:

![root txt](https://user-images.githubusercontent.com/86057471/157892512-eb91c43e-bc90-433c-949a-231462ec874c.png)



