# Library

Basic library for ripetitive tasks.

## Basic

### Get a unique name

Create a unique name, to be used when creating directories and files.

```bash
Create directory
  ${dirName}  Create a unique name
  Create directory  ${dirName}
```

### Create a local file

Create a local file with a random name under /tmp.

```bash
${file}  Create local file
Check file does not exists using lcg-utils  ${file}
```

### Execute Curl

Execute curl using the users proxy as certificate. Using

```bash
Put a file using WebDAV calling the PUT method
  ${fileName}  Run  mktemp /tmp/storm.XXXXXX
  Execute Curl  -X PUT ${fileName} https://${davEndpoint}/testers.eu-emi.eu/${fileName}
```

executes

```bash
curl --cacert ${usercert} --cert ${userproxy} --capath ${trustdir} -X PUT ${fileName} https://${davEndpoint}/testers.eu-emi.eu/${fileName}
```

and check that the command suceed.

## clientSRM based keywords

### Execute ClientSRM Command

Execute a clientSRM command. For the commands that does not need additional input, like ping

```bash
Ping the service
  Execute ClientSRM Command  ping
```
executes a

```bash
# clientSRM ping -e ${srmEndpoint}
```

checking that the command succeded (has zero output).

It allows for capturing the output

```bash
Ping the service
  ${output}  Execute ClientSRM Command  ping
  Should Contain  ${output}  SRM server successfully contacted
```

### Execute ClientSRM Command on Surl

Execute a clientSRM command that requires a Surl, like mkdir, rmdir, ptg, etc. Using

```bash
List files in storage area root
  Execute clientSRM Command on Surl srm://${srmEndpoint}/${root} -c 1
```

executes a

```bash
# clientSRM ls -e ${srmEndpoint} -s srm://${srmEndpoint}/${root} -c 1
```

checking that the command succeded (has zero output).

It allows for capturing the output

```bash
Ping the service
  ${output}  Execute ClientSRM Command  on Surl
  Should Contain  ${output}  SRM server successfully contacted
```

### Execute clientSRM Command on Surl with Token

Execute a clientSRM command that requires a Surl and a Token, like sptg, rf, sptp, pd, etc. Using

```bash
Put done a file:
  Execute clientSRM Command on Surl with Token  pd  srm://${srmEndpoint}/${root}  ${token}
```

executes a

```bash
# clientSRM pd -e ${srmEndpoint} -s srm://${srmEndpoint}/${root}  -t "${token}"
```

checking that the command succeded (has zero output).

It allows for capturing the output

```bash
Put done a file
  ${output}  Execute ClientSRM Command on Surl with Token  pd  srm://${srmEndpoint}/${root}  ${token}
  Should Contain  ${output}  SRM_SUCCESS
```

### Create directory using clientSRM

Issues a clientSRM mkdir for creating a directory of a given path.

### Try to create directory using clientSRM

Issues a clientSRM mkdir for creating a directory of a given path. This will not fail if the command fails, and returns the output.

### Remove directory using clientSRM

Issues a clientSRM rmdir for creating a directory of a given path.

### List files in directory using clientSRM

### Prepare to put

Issues a clientSRM ptp.

### Put without really putting

Issues a clientSRM ptp and the subsequent pd, without transfering the file.

### Put done

Issues a ClientSRM pd on file ${path}/${filename} using a specified ${token} and check success.

```bash
Put done  ${path}  ${filename}  ${token}
```

### Prepare to get

Issues a clientSRM ptg.

### Get unused size

Get the unused size for a storage area.
  
## lcg-utils based keywords

### List files in directory using lcg_utils

Executes a lcg-ls and returns the output.

### Check file exists using lcg-utils

Issues an lgc-ls to check that a file exists.

```bash
	Check file exists using lcg-utils  remotePath
```

### Check file does not exists using lcg-utils

Issues an lcg-ls and check that a file does not exist.

```bash
	Check file does not exist using lcg-utils  remotePath
```

### Copy-out file using lcg-utils

Issues an lcg-cp to copy a file to a StoRM instance.

```bash
  Copy-out file using lcg-utils  localePath  remotePath
```

### Copy-in file using lcg-utils

Issues an lcg-cp to copy a file from a StoRM instance.

```bash
  Copy-in file using lcg-utils  localePath  remotePath
```

## globus-utils based keywords

### Copy-out file using globus-utils

Issues a globus-url-copy to copy a file to a StoRM instance.

```bash
  Copy-out file using globus-utils  localPath  remotePath
```

### Copy-in file using globus-utils

Issues a globus-url-copy to copy a file from a StoRM instance.

```bash
  Copy-in file using globus-utils  localPath  remotePath
```

### Copy-in file using gsiftp protocol

Issues a globus-url-copy to copy a file from a StoRM instance by using its TURL and gsiftp protocol.

```bash
  Copy-in file using gsiftp protocol  turl  localPath
```

## dCache srm client based keywords

### Ping using dCache client

Ping the service executing a srmping command.

### Create directory using dCache client 

Create a directory executing a srmmkdir command. If the command fails the keyword fails.

### Try to create directory using dCache client

Create a directory executing a srmmkdir command. This will not fail if the command does not succeed and returns the output.

