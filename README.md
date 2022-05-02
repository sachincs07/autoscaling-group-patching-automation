# autoscaling-group-patching-automation
# AWS AutoScaling Group Patching Automation using Lambda function

Description :
			 This is to patch the ASG's with the latest AMI available through Marketplace or your private image from your custom account.
			 	--> This is written in python 3.9 and was developed keeping small AWS deployments where ansible tower or any other centralized system is not readily available.
			 	--> These scripts can be deployed to Lambda function and can be scheduled using eventbridge.
			 	--> The main challange faced initially was the Notification part. I took different approaches and came up with a notification part which looks into the last event in ASG's activity and based on that can send notifications or some corrective actions.
			 		In my test scneraios, Patching ASG's was not the problem but what comes after it. Few of my ASG's were failing on the userdata part of deployment process so i needed a way to notify when instance does not come healthy.
			 	--> It uses : Lambda function , EventBridge and SNS (Also IAM Role is needed with proper permissions).
Installation:
			 To install in your account please follow individial sections below :
			 	--> Create `IAM Role` : Please create a policy, please use policy.json to copy the policy document with necessary permissions you need. (Later i will create an aws Cloudformation template to build this along with everything else but for now individual files).
			 	--> Create both `lambda functions` to perform patching and notification part.
			 		** This function is going to create a newer version of AMI in Launch Template , I will add functionality to create Launch Configuration with new AMI and then update asg to use it.
			 		** Please set your ASG's to use Latest version from Launch Template.
			 		** Instance respin is outside the job and is accomplished through scheduled events.(I found this to be best as of now but will plan to add something else based on the project deadlines).
			 	--> Create an `EventBridge` rule based on your schedule , how often you want to run the job. You need two rules.
			 		--> For running the patching job.
			 		--> For Notification (I suggest to run notification to run after 2 hours just to make sure instances have enough time to spin).
Contributions:
			  Contributions can be made to this project. 

