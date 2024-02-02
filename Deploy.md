# Application Deployment Using PsExec

## Introduction
This document provides an idea of how PsExec is used for deploying an application from an agent machine to guest machines. Two approaches are outlined, with a focus on efficiency and reliability.

### Prerequisites
1. Ensure that the guest username and password match those of the agent.
2. The target executable (exe/MSI) must be located in the agent's shared folder on the network.

## Approach 1: PsExec Copy and Execute
### Command Format
```bash
psexec \\<guest_ip_address> -u <guest_username> -p<guest_password> -c -f -s "path\to\your\file.exe" <silent_command> 
```
### Description
This approach directly copies and executes the specified executable on the guest machine. It is a straightforward method that does not rely on additional commands.

### Pros
- Simplicity: Directly executes the application without multiple steps.
- Readability: The command is concise and easy to understand.
### Cons
- Dependency on PsExec arguments.

## Approach 2: PsExec with Mapping Shared Folder
### Command Format
```bash
psexec \\<guest_ip_address> -u <username> -p <password> -s cmd /c "net use Z: \\<agent_ip_address>\netinstall /user:<agent_username> <agent_password> & copy "Z:\<exe file>" "C:/netinstall/software" & net use Z: /delete & "C:\netinstall\software\<exe>" <silent_command>"
```
### Description
This approach involves mapping a shared folder from the agent machine to the guest machine (using a temporary drive Z:) and copying the executable. The Z drive is then deleted.

### Pros
- Provides more control over file copying.
- Can handle complex scenarios.
### Cons
- Involves multiple commands, potentially prone to errors.

## Conclusion
While both approaches are functional, the choice between them depends on the specific requirements and preferences. Approach 1 is simpler and more straightforward, while Approach 2 provides more control over the file copy process.
