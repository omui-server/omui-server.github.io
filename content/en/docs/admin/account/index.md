---
title: "Managing Users"
weight: 31
---

# Managing users

## LDAP Account Manager (LAM)

We use LDAP to manage users.
Since editing LDAP with CLI is not easy, we use [**LDAP Account Manager (LAM)**](https://www.ldap-account-manager.org) , which is a GUI tool to edit LDAP.

## Login to LAM

[Click here](http://172.26.43.2) to open LAM, and login with the LAM admin credentials.

## Adding users

### User information

Log in to LAM and click on "New user" in the upper left corner.
The user edit screen will appear.

You will first be asked for personal information.
Other fields can be left blank.

- **First name**
- **Last name**
- **Contact data**
  - **Email address**: User's OMU email address

![image](img/lam-new-user-personal.png)

Select "Unix" from the tabs on the left and enter the following information.
Other fields can be left blank.

- **User name**: In a format of `[research group ID][serial number]`
- **Primary group**: Select your research group ID

![image](img/lam-new-user-unix.png)

{{< hint info >}}
The home directory is automatically generated when the user logs in for the first time.
(The owner is the user, the owning group is the user's primary group.)
Therefore, there is no need for the administrator to create them manually.
{{</ hint >}}

### Set a password

Open "Set password" in the upper left corner and click "Set random password".
An initial password will be generated, so write this down somewhere.
After writing down the information, press OK.

![image](img/lam-set-password.png)

### Save

When you have completed the above, click "Save" in the upper left corner.
The user is registered in LDAP.

Once the registration is complete, please contact the user with the following credentials:

{{< hint info >}}
**OMUI Server Credentials**

- Username
- Initial password
{{</ hint >}}

## Edit users

Log in to LAM and click the edit button (pencil icon) for the user you wish to edit.
The user edit screen will open.

![image](img/lam-users-list.png)

Edit the required information and finally click "Save" in the upper left corner.

## Granting administrative privileges

To grant administrative privileges to a specific user, go to the Unix tab of the Edit User screen and add the following groups to "Additional groups".

- `omuiadmin`

Users in this group will be able to use the `sudo` command.