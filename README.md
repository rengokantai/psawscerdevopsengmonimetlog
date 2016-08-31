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
