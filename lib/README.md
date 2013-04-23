# Library

Basic library for ripetitive tasks.

## Get a unique name

Create a unique name, to be used when creating directories and files

```bash
Create directory
  ${dirName}  Create a unique name
  Create directory  ${dirName}
```

## Create a local file

Create a local file

```bash
${file}  Create local file
Check file does not exists using lcg-utils  ${file}
```

## Execute ClientSRM Command

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

## Execute ClientSRM Command on Surl

Execute a clientSRM command that requries a Surl, like mkdir, rmdir, ptg, etc. Using

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

## Execute Curl

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

## Create directory using clientSRM

Issues a clientSRM mkdir for creating a directory of a given path.

## Remove directory using clientSRM

Issues a clientSRM rmdir for creating a directory of a given path.

## Prepare to put

Issues a clientSRM ptp.

## Put without really putting

Issues a clientSRM ptp and the subsequent pd, without transfering the file.

## Prepare to get

Issues a clientSRM ptg.

## Get unused size

Get the unused size for a storage area.


  
## Check file exists using lcg-utils

Issues an lgc-ls to check that a file exists

```bash
	Check file exists using lcg-utils  remotePath
```

## Check file does not exists using lcg-utils

Issues an lcg-ls and check that a file does not exist

```bash
	Check file does not exist using lcg-utils  remotePath
```

## Copy file using lcg-utils

Issues an lcg-cp to copy a file to the SE

```bash
  Copy file using lcg-utils  localePath  remotePath
```


