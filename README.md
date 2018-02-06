# explore-aws
AWS-Lambda automation scripts will create and delete AMI's as per Tag assigned to EC2 instances

AMI Creation:
This script will search for all instances having a tag with "BackupDaily" or "backupdaily" on it. As soon as we have the instances list, we loop through each instance and create an AMI of it. Also, it will look for a "Retention" tag key which will be used as a retention policy number in days. If there is no tag with that name, it will use a 7 days default value for each AMI. After creating the AMI it creates a "DeleteOn" tag on the AMI indicating when it will be deleted using the Retention value and another Lambda function 

AMI Retention:
This script will search for all instances having a tag with ['backupdaily', 'BackupDaily', 'backupweekly', 'BackupWeekly'] on it. As soon as we have the instances list, we loop through each instance
and reference the AMIs of that instance. We check that the latest daily backup succeeded then we store every image that's reached its DeleteOn tag's date for deletion. We then loop through the AMIs, deregister them and remove all the snapshots associated with that AMI.
