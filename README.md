# LinuxCommands

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
### Passwordless entry set up
copy ssh keys -> passwordless entry
```
  cat ~/.ssh/id_rsa.pub | ssh user@123.45.56.78 "cat >> ~/.ssh/authorized_keys"
  cat ~/.ssh/id_rsa.pub | ssh root@vvlhost01 "cat >> ~/.ssh/authorized_keys"
```
