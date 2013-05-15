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

### Create local file with checksum that starts with zero

Create a local file with a random name under /tmp with checksum value that starts with '0'.

```bash
${file}  Create local file with checksum that starts with zero
Check file does not exists using lcg-utils  ${file}
```

### Execute Curl with options

Execute curl on the specified URL, eventually using the options passed, and then checks if the command succeeds.
As example, using:

```bash
WebDAV MKCOL with voms proxy
  [Setup]  Init certificate and voms proxy  test0  ${vo}
  ${dirname}  Get a unique name
  ${options}  Set variable  --verbose -X MKCOL --cert ${userproxy} --capath ${trustdir}
  ${url}  Set variable  https://${davSecureEndpoint}/${vomsproxyRWStorageArea}/${dirName}
  ${output}  Execute Curl with options  ${url}  ${options}
```

executes:

```bash
curl --verbose -X MKCOL --cert ${userproxy} --capath ${trustdir} https://${davSecureEndpoint}/${vomsproxyRWStorageArea}/tmp.tlour26193
```

and check that the command succeed.

### Build surl

Retrieves a valid SURL in query form, builded from passed ${storageArea} and ${relativePath}.
For exemple, using:

```bash
  Build surl  storageAreaName  /path/to/file
```

retrieves:

```
  srm://${srmEndpoint}/srm/managerv2?SFN=/storageAreaName/path/to/file
```

### Build simple surl

Retrieves a valid SURL in simple form, builded from passed ${storageArea} and ${relativePath}.
For exemple, using:

```bash
  Build simple surl  storageAreaName  /path/to/file
```

retrieves:

```
  srm://${srmEndpoint}/storageAreaName/path/to/file
```

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

### Perform mkdir using clientSRM

Using clientSRM, launches a SRM _mkdir_ command on a specified _surl_ that has to point to a non existent directory, eventually specifying some extra _options_. For example, using:

```bash
  ${surl}  Build surl  storageAreaName  /path/to/newdir
  Perform mkdir using clientSRM  ${surl}
```

a /path/to/newdir directory is created.

### Perform rm using clientSRM

Using clientSRM, launches a SRM _rm_ command on a specified _surl_ that has to point to an existent file, eventually specifying some extra _options_. For example, using:

```bash
  ${surl}  Build surl  storageAreaName  /path/to/existent/file
  Perform rm using clientSRM  ${surl}
```

the existent file /path/to/existent/file is removed.

### Perform rmdir using clientSRM

Using clientSRM, launches a SRM _rmdir_ command on a specified _surl_ that has to point to an existent directory, eventually specifying some extra _options_ (in case directory is not empty, you have to add -r option). For example, using:

```bash
  ${surl}  Build surl  storageAreaName  /path/to/existent/directory
  Perform rm using clientSRM  ${surl}  -r
```

the existent directory /path/to/existent/directory (and eventually all its sub-files) is removed.

### Perform ping using clientSRM

Perform a ping command on the configured SRM endpoint.

### Perform ptp using clientSRM

### Perform sptp using clientSRM

### Perform pd using clientSRM

### Perform ptg using clientSRM

### Perform sptg using clientSRM

### Perform rf using clientSRM

### Perform ls using clientSRM

### Detailed ls using clientSRM

Issues a clientSRM ls with -l option of a given path

### Get unused size using clientSRM

Get the unused size for a storage area.

### Get space metadata using clientSRM

### Reserve space using clientSRM

### Release space using clientSRM

### Create directory using clientSRM

Issues a clientSRM mkdir to create a directory identified by the storage-area name and a relative path.

### Remove empty directory using clientSRM

Issues a clientSRM rmdir to delete an empty directory identified by the storage-area name and a relative path.

### Remove not empty directory using clientSRM

Issues a clientSRM rmdir to delete a non empty directory identified by the storage-area name and a relative path.

### Remove file using clientSRM

Issues a clientSRM rm to delete an existent file identified by the storage-area name and a relative path.

### Put without really putting using clientSRM

Issues a clientSRM ptp and the subsequent pd, without transfering the file.

### List files in directory using clientSRM

### Get space token using clientSRM
  
### Init certificate and voms proxy

### Init certificate and plain proxy

### Init certificate with unencrypted key

### Clear all credentials


## lcg-utils based keywords

### List files in directory using lcg_utils

Executes a lcg-ls and returns the output.

### Check file exists using lcg-utils

Issues an lgc-ls to check that a file exists.

```bash
	Check file exists using lcg-utils  surl
```

### Check file does not exists using lcg-utils

Issues an lcg-ls and check that a file does not exist.

```bash
	Check file does not exist using lcg-utils  surl
```

### Copy-out file using lcg-utils

Issues an lcg-cp to copy a file to a StoRM instance.

```bash
  Copy-out file using lcg-utils  localePath  surl
```

### Copy-in file using lcg-utils

Issues an lcg-cp to copy a file from a StoRM instance.

```bash
  Copy-in file using lcg-utils  remotePath  localePath
```

### Copy file using lcg-utils

Issues an lcg-cp to copy a file identified by a remote source SURL to a remote destination also identified by another SURL.

```bash
  Copy file using lcg-utils  remoteSrcSURL  remoteDestSURL
```

## globus-utils based keywords

### Copy-out file using globus-utils

Issues a globus-url-copy to copy a file to a StoRM instance.

```bash
  Copy-out file using globus-utils  localPath  remoteStorageArea  remotePath
```

### Copy-in file using globus-utils

Issues a globus-url-copy to copy a file from a StoRM instance.

```bash
  Copy-in file using globus-utils  remoteStorageArea  remotePath  localPath
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

### Remove directory using dCache client

### Try to remove directory using dCache client

### Remove file using dCache client

### Try to remove file using dCache client


## Credentials management keywords

### Use certificate

### Use certificate with unencrypted key

### Stop using certificate

### Get options list

### Get proxy info

### Create proxy

### Create plain proxy

### Destroy proxy

### Create voms proxy

