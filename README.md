AWS Chaos Monitor
=================

The goal of this project is a set of tools for dealing with large numbers of AWS accounts across multiple regions. It provides a number of shell and python scripts for extracting useful and actionable .json output from AWS CLI tools and indexing them within Elastic Search for search and analysis.

It was primarily developed on Debian Linux 7.0 but should work on anything if the supporting components are installed.

Design Goals
============
* Minimal configuration
* Simple support of arbitrary AWS accounts and applications


External Dependencies
=====================

* AWS CLI Tools - http://aws.amazon.com/cli/
* jq - http://stedolan.github.io/jq/
* Elastic Search - http://www.elasticsearch.org/



Configuration
=============

Modify the environment variables to match your system

```
mfranz@deb-t61:~/awschamon$ cat awschamon-vars.sh 
export AWSKEYDIR="/home/mfranz/.secret/awskeys"
export AWSCHAMONHOME="/home/mfranz/awschamon"
export AWSCHAMONDATA=$AWSCHAMONHOME/var
export AWSCHAMONCONF=$AWSCHAMONHOME/etc
export PATH=$PATH:$AWSCHAMONHOME/bin
export PATH=$PATH:$AWSCHAMONHOME/sbin
```

Add AWS a shell script to export the usual AWS CLI/Boto environment variables
* AWS_ACCESS_KEY_ID
* AWS_SECRET_ACCESS_KEY




```
mfranz@deb-t61:~/awschamon$ ls -al ~/.secret/awskeys/meh.sh 
-rwxr--r-- 1 mfranz mfranz 120 Nov 24 17:06 /home/mfranz/.secret/awskeys/meh.sh
```
