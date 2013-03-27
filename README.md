# StoRM testsuite

# Get prepared


## Robot Framework 

This testsuite uses [Robot Framework](https://code.google.com/p/robotframework/). For SL*, 
Robot Framework is not on a repository, and it is needed to manually install it

First install python 2.6

    yum install python 26

then dowload Robot and inside the root run

    sudo python26 setup.py install

## VOMS clients

The voms clients package installed, i.e. voms-proxy-* commands must be available.

## Getting the testsuite 

Checkout the code using the following command:

    git clone git://github.com/valerioventuri/storm-testsuite.git

## Run tests

Execute the Robot Framework command-line passing the storm frontend endpoint and the root of the storage area  
        
    pybot --variable endpoint:omii001-vm04.cnaf.infn.it --variable root:testers.eu-emi.eu pythonpath lib tests.txt
