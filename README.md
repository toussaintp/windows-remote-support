<p align="center">
<img width="447" height="447" alt="logo" src="https://github.com/user-attachments/assets/2346103d-ff8a-40cb-8f5f-8b48e0ece937" />
</p>

<h1>Windows Remote Desktop & Remote Assistance</h1>

<h1> Project Overview</h1>

This project demonstrates the configuration and testing of Windows Remote Desktop and Windows Remote Assistance in a Hyper-V virtualized environment. I configured remote-access permissions, created an authorized local user, established an RDP connection, configured Remote Assistance, and tested remote viewing and shared control. <br />

<h1>1. Business Scenario</h1>

An IT support technician may need to access a user's workstation remotely to perform administrative tasks or troubleshoot technical problems.

In this project, I simulated two common remote-support scenarios:

1. **Remote Desktop:** An authorized user remotely signs into a Windows workstation and controls the computer as if physically present.
2. **Remote Assistance:** A user invites a trusted technician to view the existing desktop session and, with permission, take shared control for troubleshooting.

The goal was to configure, secure, test, and compare both remote-support methods in a controlled lab environment. <br />

<h1>2. Lab Environment</h1>

| Component                  |  Environment                 |
| -------------------------- | -------------------------------- |
| Physical computer          | Windows laptop                   |
| Virtualization             | Microsoft Hyper-V                |
| Guest OS                   | Windows 10 Enterprise Evaluation |
| VM networking              | Hyper-V Default Switch           |
| VM IPv4                    | `172.19.85.239`                  |
| Physical host adapter IPv4 | `172.19.80.1`                    |
| Remote protocol            | RDP                              |
| RDP port                   | TCP 3389                         |
| Remote account             | Local Windows account            |

<p>
<img width="633" height="101" alt="02-ipv4-address" src="https://github.com/user-attachments/assets/8de77b2c-2259-430c-926b-18a0ad015881" />
</p>
The IPv4 configuration of the Windows virtual machine was identified using `ipconfig`. The virtual machine was connected through the Hyper-V Default Switch.

 <br />

 <h1>3. Network Configuration</h1>
 Remote Desktop was enabled on the Windows system to allow authorized remote connections.

Windows Network Level Authentication (NLA) was also enabled. NLA requires users to authenticate before a full Remote Desktop session is established, providing an additional layer of security for remote connections.

Physical Windows Laptop
          │
          │ Hyper-V networking
          ▼
Windows 10 Enterprise VM
          │
          └── RDP TCP/3389 
<p>
 <img width="893" height="287" alt="01-remote-desktop-enabled png" src="https://github.com/user-attachments/assets/0881e446-d630-44d1-b8ab-67910ccb4805" />
 <p>        
          <br />


<h1>4. Verifying the RDP Port</h1>

I reviewed the Windows Remote Desktop configuration and verified that the system was using the default Remote Desktop Protocol port:

**TCP 3389**

Understanding the service port is useful when troubleshooting Remote Desktop connectivity, firewall rules, and network access.

<p>
<img width="857" height="233" alt="03-remote-desktop-port" src="https://github.com/user-attachments/assets/c64a1452-43fc-42a1-9c7c-8c9402574021" />
 <p>  
<br />

<h1>5. Configuring Remote User Access</h1>

A dedicated local account named `RDP-Lab` was created for testing remote access.

Rather than allowing unrestricted access, the account was explicitly authorized through the Windows **Remote Desktop Users** configuration.

This demonstrates the principle that remote access should be granted only to authorized accounts that require it. 

<p>
<img width="367" height="331" alt="04-authorized-rdp-user" src="https://github.com/user-attachments/assets/64971af7-301d-4763-b415-b06e8551e247" />
 <p>  
<br />

<h1>6. Establishing the RDP Session</h1>

From the physical Windows computer, I launched Remote Desktop Connection and connected to the Windows virtual machine using its network address.

The dedicated `RDP-Lab` account was used to authenticate to the remote computer.

During the connection process, Windows detected that another user session was already active on the remote computer. 

<p>
<img width="900" height="777" alt="06-existing-user-warning png" src="https://github.com/user-attachments/assets/b7f67507-3c0d-483b-ad27-ef6e4080192f" />
 <p> 
<br />

<h1>7. Validating the RDP Connection</h1>

After authentication, the Remote Desktop session was successfully established.

To validate that I was operating inside the remote session, I opened Notepad on the remote computer and entered a test message confirming successful connectivity.

The Remote Desktop Connection window displayed the remote system's IP address, providing additional confirmation that the session was active. 

<p>
<img width="1108" height="441" alt="07-successful-rdp-session png" src="https://github.com/user-attachments/assets/c39da239-4a20-4bcc-984a-d0abd274fe75" />
 <p> 
<br />

<h1>8. Configuring Windows Remote Assistance</h1>

Windows Remote Assistance was enabled to simulate a help-desk scenario in which a user requests assistance from a trusted technician.

Unlike Remote Desktop, Remote Assistance allows the user and helper to participate in the same desktop session, making it useful for collaborative troubleshooting. 

<p>
<img width="398" height="468" alt="08-remote-assistance-enabled" src="https://github.com/user-attachments/assets/ac5526c3-88ce-4f9e-9699-afa58e589719" />
 <p> 
<br />

<h1>9. Configuring Remote Assistance Invitations</h1>

I reviewed the Remote Assistance invitation settings and verified that remote control was permitted.

The default invitation expiration period in my environment was configured for **6 hours**.

Invitation expiration limits reduce the amount of time an unused Remote Assistance invitation remains valid. 

<p>
<img width="401" height="469" alt="09-invitation-duration png" src="https://github.com/user-attachments/assets/75082043-f117-4c54-848a-eb8eb8e8b512" />
 <p> 
<br />

<h1>10. Configuring Remote Assistance Invitations</h1>

Windows Remote Assistance provided multiple methods for inviting a trusted helper.

The available options included:

- Saving the invitation as a file
- Sending the invitation through a compatible email application
- Easy Connect, when available

The invitation-file method was used to initiate the Remote Assistance workflow. 

<p>
<img width="401" height="469" alt="09-invitation-duration png" src="https://github.com/user-attachments/assets/75082043-f117-4c54-848a-eb8eb8e8b512" />
 <p> 
<br />

<h1>11. Establishing the Remote Assistance Session</h1>

After the invitation was opened by the helper, Windows requested authorization from the user before allowing the remote connection.

This consent requirement helps prevent an unauthorized helper from connecting to the user's desktop simply by initiating a connection. <br />

<h1>12. Requesting Shared Control</h1>

Initially, Remote Assistance allowed the helper to view the user's desktop.

To interact with the remote computer, the helper requested control of the desktop. Windows then prompted the user to explicitly approve shared control.

After permission was granted, the helper could interact with the desktop and assist with troubleshooting. <br />

<h1>13. Remote Desktop vs. Remote Assistance</h1>

| Feature | Remote Desktop | Remote Assistance |
|---|---|---|
| Primary Purpose | Remote system access and administration | Collaborative technical support |
| Authentication | Authorized Windows account | User-generated invitation and authorization |
| User Interaction | Remote user operates the session | User and helper can view the same desktop |
| Control | Remote user controls the session | Helper must request control |
| User Consent | Account authorization allows connection | User explicitly approves the assistance connection |
| Typical Use Case | Accessing another Windows computer remotely | Help-desk technician assisting a user |
| Default RDP Port | TCP 3389 | Dynamically assigned for Remote Assistance | <br />

<h1>14. Troubleshooting & Observations</h1>

### ICMP Connectivity Testing

During initial connectivity testing between the physical computer and virtual machine, ping requests timed out.

However, Remote Desktop connectivity was subsequently established successfully.

This demonstrated that failure of an ICMP echo request does not necessarily mean that all network communication between two systems is unavailable. Connectivity should be tested using the protocol or service relevant to the problem being investigated.

### Remote Desktop Certificate Warning

During the initial Remote Desktop connection, Windows displayed a warning that the identity of the remote computer could not be verified.

Because this was a controlled lab environment and I had verified the destination system, I proceeded with the connection.

This reinforced the importance of reviewing certificate and identity warnings rather than automatically accepting them.

### Existing User Session

When establishing the RDP session, Windows reported that another user was already signed in and would be disconnected if the new session continued.

This demonstrated how Windows client operating systems manage interactive Remote Desktop sessions.

### Local Account Authentication

The dedicated local account was identified using the remote computer's account context when authenticating to the VM.
This reinforced the distinction between local Windows accounts and Microsoft/domain accounts during remote authentication.
 <br />

<h1>15.Security Considerations</h1>

This project demonstrated several security considerations associated with remote access:

- Remote Desktop should only be enabled when required.
- Only authorized users should be granted remote access.
- Strong passwords should be used for remote-access accounts.
- Network Level Authentication should be used when supported.
- Certificate and identity warnings should be reviewed before continuing.
- Remote Assistance should only be provided to or accepted from trusted individuals.
- Remote Assistance requires user consent before a helper can connect.
- Shared desktop control requires additional user approval.
- Invitation files and Remote Assistance passwords should not be publicly exposed. <br />

<h1>16. Validation</h1>

| Test | Result |
|---|---|
| Remote Desktop enabled | ✅ Pass |
| Network Level Authentication enabled | ✅ Pass |
| RDP port 3389 identified | ✅ Pass |
| VM IPv4 configuration identified | ✅ Pass |
| Dedicated RDP user authorized | ✅ Pass |
| Remote Desktop authentication completed | ✅ Pass |
| Remote Desktop session established | ✅ Pass |
| Remote Assistance enabled | ✅ Pass |
| Remote Assistance invitation created | ✅ Pass |
| Remote Assistance connection authorized | ✅ Pass |
| Shared desktop control requested and approved | ✅ Pass | <br />

<h2>17. Skills Demonstrated</h2>

- Windows Administration
- Remote Desktop Protocol (RDP)
- Windows Remote Assistance
- Remote Support
- Local User Account Management
- Remote Access Authorization
- Network Level Authentication (NLA)
- IPv4 Network Configuration
- TCP/IP
- Hyper-V Virtualization
- Windows Security
- Remote Troubleshooting
- Technical Documentation
  <br />

  <h2>18. Lessons Learned</h2>

This project strengthened my understanding of Windows remote administration and remote technical support.

I learned how to configure Remote Desktop, authorize specific users for remote access, identify the network information required for an RDP connection, and validate a successful remote session.

I also learned the operational difference between Remote Desktop and Remote Assistance. Remote Desktop is designed primarily for remotely accessing another Windows system, while Remote Assistance is better suited to collaborative troubleshooting because the user remains involved and must authorize both the connection and shared control.

The troubleshooting performed during the project also reinforced the importance of testing the specific service being used rather than relying on a single connectivity test such as ping.
  <br />

