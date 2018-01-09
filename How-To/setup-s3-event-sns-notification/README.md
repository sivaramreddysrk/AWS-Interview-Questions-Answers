# Amazon S3 Event Notifications
The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. 

## Configuring Notifications
To enable notifications, you must,
- First, Add a notification configuration(`SNS`) identifying the events you want Amazon S3 to publish,
  - Subscribe to SNS with `email` notification
- Second, Update the destinations where you want Amazon S3 to send the event notifications

### Granting Permissions for S3 to Publish Messages to an SNS Topic
IAM policy that needs to be attached to the destination SNS topic,
```json
{
 "Version": "2008-10-17",
 "Id": "example-ID",
 "Statement": [
  {
   "Sid": "s3-event-notifier",
   "Effect": "Allow",
   "Principal": {
     "Service": "s3.amazonaws.com"
   },
   "Action": [
    "SNS:Publish"
   ],
   "Resource": "<UPDATE-YOUR-SNS-ARN-HERE>",
   "Condition": {
      "ArnLike": {          
      "aws:SourceArn": "arn:aws:s3:*:*:<UPDATE-YOUR-BUCKET-NAME-HERE>"
    }
   }
  }
 ]
}