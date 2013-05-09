# Space Management tests

Tests that check StoRM space management, such as used or free disk space information, storage area's quota, etc..

### Space token used space is update

**Unique ID** = b740fb

**RFC unique ID** = [https://storm.cnaf.infn.it:8443/redmine/issues/109](https://storm.cnaf.infn.it:8443/redmine/issues/109)

**Tags** = storm-client, lcg-utils, gst, regression

**Bug**:

StoRM does not provides updated used space value for Space Token. This problem is due to a bug in the update of the used space after the the srmPutDone operation.

**Test description**:

Given a Space Token ST and a SURL that resides on ST pointing to a not existent file, verify that inspecting the unused space of the ST before and after a non empty file has been stored on the SURL the ST used space value is updated accordingly to the size of the new file.

**Test steps**:

1. Perform an srmGetSpaceMetadata on ST;
2. Extract from the output the unusedSize US1 values;
3. Perform an srmPrepareToPut on the SURL specifying ST as targetSpaceToken; 4. transfer the file;
5. Perform an srmPutDone on the SURL;
6. Perform an srmGetSpaceMetadata on ST;
7. Extract from the output the unusedSize US2 values/

**Input**:

- a *Space Token* refering to a certain space available on the StoRM instance; 
- a non empty file;
- a SURL pointing to a non existing file residing on ST.

**PASS** : the test is passed if the result of US1 minus US2 matches the size of the new file. 

**FAIL** : otherwise.