#### psawscerdevopsengmonimetlog
#####Getting Started with CloudWatch
######4 CloudWatch Overview
Instance->status checks tab
- System status checks. Hypervisor level. Monitor the aws system required to use this instance and ensure they are functioning
- Instance status checks. Monitor software network cofifuration for this instance  
metric store from 1h to 2weeks  
create a dashboard->save, auto refresh


######5
EC2->create->step3->select enable cloudwatch detailed monitoring(Can be enable after EC2 instance created  

aws cli cmd:
```
aws ec2 monitor-instances --instance-ids i-123 
```

######7 Viewing and Searching for Metrics
```
aws cloudwatch list-metrics --namespace 'AWS/SNS'
```
######8 Getting statistics
3600 seconds
``` 
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization --period 3600 --statictics Maximumm --dimensions 'Name=InstaneId,Value=i-1234' --start-time 2016-01-01T11:11:11 --end-time 2016-01-03T12:12:12
```
another example
```
aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name DiskWriteBytes --period 360 --statictics Sum --dimensions 'Name=AutoScalingGroupName,Value=ke' --start-time 2016-01-01T11:11:11 --end-time 2016-01-03T12:12:12
```

######12 Preparing EC2 Instances for custom monitoring

generate policy:Service=amazon cloudwatch actions=GetMetricStatictics, ListMetrics,PutMetricData  
Service=amazon ec2 actions=DescribeTags  
Add these 2 policys to a role.(that means we have privileges when executing cmds in this instance, not local machine)  
create a win2012 instance with this role.  
step4, execute script in the gist
```
https://gist.github.com/mikepfeiffer
```
copy
```
<powershell>
iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
choco install python -y
(new-object net.webclient).DownloadFile('https://s3.amazonaws.com/aws-cli/AWSCLI64.msi','c:\AWSCLI64.msi')
msiexec.exe /i 'C:\AWSCLI64.msi' /qn
</powershell>
```
for centos(amz ami)
```
#!/bin/bash
yum install perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https -y
curl http://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.1.zip -O
unzip CloudWatchMonitoringScripts-1.2.1.zip
rm CloudWatchMonitoringScripts-1.2.1.zip
```
