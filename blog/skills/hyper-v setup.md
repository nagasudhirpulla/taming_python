# Hyper-V for creating VMs in Windows
-   Hyper-V is a type-1 virtualization platform in windows that can be used to create and manage virtual machines (VMs) directly in the Windows operating system without installing any third party hypervisors like virtual box.
-   Hyper-V is a type-1 hypervisor because when it is enabled, it effectively transforms the host operating system into a virtual machine running on top of the Hyper-V hypervisor.
-   Virtual machines of many Windows and Linux based operating systems are supported in Hyper-V

## Check if virtualization is enabled in Task Manager’s performance tab

Virtualization in CPU should be enabled for Hyper-V. It can be checked in Task Manager

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/db487084-9b79-45b5-9d4e-ae9bdeb60b0b/Untitled.png)

## Add Hyper-V feature for Windows home edition

-   Hyper-V is not present in Windows home edition by default.
-   It can be enabled by running a batch script with the following text

```powershell
rem install_hyperv.bat file

pushd "%~dp0"

dir /b %SystemRoot%\\servicing\\Packages\\*Hyper-V*.mum >hyper-v.txt

for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\\servicing\\Packages\\%%i"

del hyper-v.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL

pause

```

## Enable Hyper-v in windows features

-   For windows desktop OS, Hyper-V feature can be enabled in Windows Features as shown below.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/0bc84b49-9b8d-4c41-a7e8-41f4b561fd1e/Untitled.png)

-   For Windows servers, the Hyper-V role should be enabled to user Hyper-V.

## Hyper-v manager

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/d9741211-05e7-42aa-836d-0abd6c91b424/Untitled.png)

-   Hyper-V Manager provides a UI to manage the virtual machines
-   Search for Hyper-V manager and run as administrator
-   You can also open it from command line by opening command prompt as administrator and type `virtmgmt.msc`

## Create a VM from ISO file in Hyper-V manager

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/47bc180f-53a7-4b80-9f7a-c606464a9163/1758d310-79e7-4539-8aa9-84f233850cc1.png)

-   Download ISO for the OS. For this example, we are downloading windows server 2022 evaluation edition. The OS is free to use for about 18 days
-   In the right pane, click New → Virtual Machine. Specify the new VM name and also if required specify another folder location for storing VM

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/60fdfdcc-68f2-4ab5-9697-a17178937988/Untitled.png)

-   Specify VM Generation (Generation 2 is preferred)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/89e62924-30dc-4183-a0a0-6521ac875b19/Untitled.png)

-   Specify Start-up RAM (generally keep it at least 1024 MB). Dynamic Memory option can also be used to allocate only the required amount of RAM to VM while it is running

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/2be08bcd-e939-4cdc-878d-fc55ecf7dc34/Untitled.png)

-   Configure virtual switch for VM network adapter

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/af852cb6-2877-4730-a4f6-2010838686b4/Untitled.png)

-   Configure virtual hard disk size for VM

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/a1a0e8ca-94e7-48ac-9158-2b94c5c50ffa/Untitled.png)

-   Select ISO file for VM operating system. Create a new VM.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/e8aa2a1a-3ea6-493a-9d57-385605249d65/Untitled.png)

-   Start the new VM from Hyper-V Manager.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/d59201d0-d7e8-488e-b239-bdc480132fc7/Untitled.png)

-   Connect to VM after VM has started

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/fe8956b1-2ee2-49b5-aadd-4cba9c6d1bc3/Untitled.png)

-   Select the required server setup options for the first time booting

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/94c8f05a-8c36-4266-acf6-f21865393914/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/1baef821-ba16-4a5b-946d-33d3d80760aa/Untitled.png)

-   Now the VM is setup and can be managed from Hyper-V Manager.

## Stop and start the Hyper-V service

-   Click “Stop Service” in the right pane of Hyper-V Manager to stop Hyper-V service
-   To start the service start the windows service “Hyper-V Virtual Machine Management” in services.msc

## References

-   Explanation on why Hper-V is a type 1 hypervisor - [https://superuser.com/a/836123](https://superuser.com/a/836123)
-   Hyper-V official documentation - [https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjM1NDg3OTY4XX0=
-->