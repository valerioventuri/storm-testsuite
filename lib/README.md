# Library

Basic library for ripetitive tasks.

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

