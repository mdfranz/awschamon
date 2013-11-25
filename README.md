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

Modify the environment variables in __awschamon-vars.sh__ to match your system

```
mfranz@deb-t61:~/awschamon$ cat awschamon-vars.sh 
export AWSKEYDIR="/home/mfranz/.secret/awskeys"
export AWSCHAMONHOME="/home/mfranz/awschamon"
export AWSCHAMONDATA=$AWSCHAMONHOME/var
export AWSCHAMONCONF=$AWSCHAMONHOME/etc
export PATH=$PATH:$AWSCHAMONHOME/bin:$AWSCHAMONHOME/sbin
```

Add AWS a shell script to export the usual AWS CLI/Boto environment variables
* AWS_ACCESS_KEY_ID
* AWS_SECRET_ACCESS_KEY




```
mfranz@deb-t61:~/awschamon$ ls -al ~/.secret/awskeys/meh.sh 
-rwxr--r-- 1 mfranz mfranz 120 Nov 24 17:06 /home/mfranz/.secret/awskeys/meh.sh
```


Sample Run
==========

Assumption dependencies are installed and environment variables are properly set you can begin indexin


```
mfranz@deb-t61:~/awschamon$ sbin/update-objects.sh 
Found keys
{
  "ok" : true,
  "status" : 200,
  "name" : "Ardroman",
  "version" : {
    "number" : "0.90.7",
    "build_hash" : "36897d07dadcb70886db7f149e645ed3d44eb5f2",
    "build_timestamp" : "2013-11-13T12:06:54Z",
    "build_snapshot" : false,
    "lucene_version" : "4.5.1"
  },
  "tagline" : "You Know, for Search"
}Found elasticsearch cluster
Indexing REDACTED/securitygroups/us-east-1-1385336687
Indexing REDACTED/instances/us-east-1-1385336687
Indexing REDACTED/users/us-east-1-1385336687
Indexing REDACTED/virtual-mfa-devices/us-east-1-1385336687
Indexing REDACTED/vpcs/us-east-1-1385336687
Indexing REDACTED/subnets/us-east-1-1385336687
Indexing REDACTED/routetables/us-east-1-1385336687
Indexing REDACTED/addresses/us-east-1-1385336687
Indexing REDACTED/loadbalancers/us-east-1-1385336687
Indexing REDACTED/securitygroups/us-west-1-1385336687
Indexing REDACTED/instances/us-west-1-1385336687
Indexing REDACTED/users/us-west-1-1385336687
Indexing REDACTED/virtual-mfa-devices/us-west-1-1385336687
Indexing REDACTED/vpcs/us-west-1-1385336687
Indexing REDACTED/subnets/us-west-1-1385336687
Indexing REDACTED/routetables/us-west-1-1385336687
Indexing REDACTED/addresses/us-west-1-1385336687
Indexing REDACTED/loadbalancers/us-west-1-1385336687
```

The follwoing conventions were used. I'm new to ElasticSearch so these may change and I'm not sure they even make sense:

* Indexes are creates for each AWS account ID
* Document types correspond to the type of AWS resource that will be dumped (security groups, instances, IAM users, subnet, etc.)
* Document ID is region + epoch time
