
## SED Commands
### Sed to replace complex characters 
```
sed 's/\#com\.ibm\.ssl\.enabledCipherSuites\=/com\.ibm\.ssl\.enabledCipherSuites\=SSL_ECDHE_RSA_WITH_AES_128_GCM_SHA256/1'
sed -e 'H;1h;$!d;x; s///g1; ' old.txt > new.txt
```
### remove the prop file loading lines from all the scripts
```
sed -i '/Loading the property file/,+7d' *.sh
```
### insert loadProps function call
```
sed -i 's/^if \[\[ \$# -eq 1 && -e .*dirname .*]]; then/loadProps $1/g' *.sh
```
### insert source lib execution
```
sed -i '/^loadProps/s/^/source `dirname $0`\/scriptLibs.sh\n/' *.sh
sed -i '//s///' *.sh
```
## Perl Onliners 

### Replace all the jython file home folders
```
perl -p -i -e 's/\${JYTHON_FILE}/JY\/\${JYTHON_FILE}/g' *.sh
perl -p -i -e 's/nbs//g' *.PROPERTIES
```
### perl to replace last character with a string
```
perl -p -i -e 's/>$/ / if /<Server Name=".*">/' prod.xml
perl -p -i -e 's/$/ConnectTimeout="5" LoadBalanceWeight="2" MaxConnections="-1">/ if /<Server Name=".*"/' prod.xml

perl -p -i -e 's/@([a-zA-Z_])@/ print $1' TE
perl -p -i -e 's/log4j\.appender\.R\.File.*/log4j.appender.R.File = "$ENV{SCRIPT_LOG}"/' ${LOG4JFILE}
```
### perl to replace with variable substitution
```
replaceVal=$(echo "Test_Url":"https://abc.com/v1", | perl -ne '/Test_Url.?(http.*),/ && print "$1\n"')
perl -p -i -e 's/TEST_URL.*/TEST_URL=$ENV{replaceVal}/g' sample.txt
```
### perl to match 2 patterns and store them in 2 shell variables
```
read -r var1 var2 <<<  $(perl -n -e '$e = $1, $f = $2 if /Approval To (regex1) - (.*) or/;  END{ print "$e $f" }' sample_file.txt)
echo $var1 #prints regex1 pattern matches
echo $var2 #prints regex patterns matchin anything from "- " to "or"
```

### Passwordless ssh login into a linux host
Enter the following on the host from where you want to connect to a remote host.
Lets say you want to connect from host A to a remote-host B
Enter the following on host A, and accept all the default by pressing enter key.
```
ssh-keygen
```
Now copy the file onto the remote-host B, bear in mind you will be prompted for a password for this below command
```
ssh-copy-id -i .ssh/id_rsa.pub -p 2022 user@remote-host-B
```

Or you can copy ssh keys using the following commands, bear in mind you will be prompted for a password for this below command
```
  cat ~/.ssh/id_rsa.pub | ssh user@host-B "cat >> ~/.ssh/authorized_keys"
```
After the keys are copied to the remote host using one of the above commands, try the ssh again.
If configured correctly it shouldnt prompt you for a password this time around.
```
ssh -p 2022 user@host-B
ssh user@host-B
```
