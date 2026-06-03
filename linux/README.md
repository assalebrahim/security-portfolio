# Linux System Hardening - User Account Security

### Overview
This document explores techniques used to improve Linux system security.

## Task 1 - User Accounts
  ### The Principle of Least Privilege
  Users should only be granted the minimum permissions required to perform their tasks.

  Best practices:
  * Avoid giving administrative privileges unless required.
  * Assign users only to necessary groups.
  * Remove unused accounts and permissions.

  Why this matters:
  Reducing privileges limits the impact of user mistakes, privilege abuse, and account compromise.


  ### Restrict sudo Privileges.
  Users with sudo permissions can execute commands as the root user. Improper sudo access increases security risk.

  Best practices:
  * Grant access only to required commands or binaries.
  * Avoid broad sudo permissions unless necessary.
  * Restrict execution paths to reduce abuse through chained binaries or [GTFOBins](https://gtfobins.org/) techniques.
  * Use sudoedit for file editing instead of granting direct editor execution with sudo.
      Eg:
      Intead of allowing:
      > sudo vim /path-to-file
      Prefer:
      > sudoedit /path-to-file\

    Why this matter - some binaries can be abused for privilege escalation or shell escape attacks by running its functionality that can launch other commands.

    
    ### Disable Root Shell Login.
    Direct root login should generally be disabled.

    One approach is assigning a non-login shell to the root account (/usr/sbin/nologin).
    This prevents interactive shell access.

    Why this matters - Disabling root login reduces attack surface and encourages accountability through sudo-based privilege escalation.


    ### Enforce Strong Password Policies
    Password policies can be strengthened through PAM (Pluggable Authentication Modules).

    Recommended controls:
    * Password complexity requirements
    * Minimum password length
    * Password expiration policies
    * Password history - to prevent password reuse
   
    Why this matters - Weak passwords increase the risk of brute-force attacks, password reuse attacks, and credential compromise.


    ### Lock Down Home Directories
    Home directories should follow the principle of least privilege.

    Best practices:
    * Restrict unnecessary access to user home directories.
    * Remove permissions for other users when not required.
    * Allow access only to the owner and required group.
   
    Why this matters - Improper file permissions may expose sensitive files, credentials, SSH keys, or application data.



## Task 2 - Firewall
