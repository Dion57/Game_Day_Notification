# NBA Game Day Notifications / Sports Alerts System  

## Project Overview  
This project is an alert system that sends real-time NBA game day score notifications to subscribed users via SMS/Email. It leverages **Amazon SNS**, **AWS Lambda**, **EventBridge**, and **NBA APIs** to provide sports fans with up-to-date game information.  

The project demonstrates the principles of cloud computing and efficient notification mechanisms, showcasing the integration of serverless AWS services with external APIs.  

---

## Features  
- Fetches live NBA game scores using an external API.  
- Sends formatted score updates to subscribers via SMS/Email using Amazon SNS.  
- Automated notifications with scheduling using Amazon EventBridge.  
- Follows security best practices by implementing least privilege for IAM roles.  

---

## Prerequisites  
- Free account with subscription and API Key at [SportsData.io](https://sportsdata.io).  
- Personal AWS account with a basic understanding of AWS and Python.  

---

## Technical Architecture  

### Technologies  
- **Cloud Provider:** AWS  
- **Core Services:** SNS, Lambda, EventBridge  
- **External API:** NBA Game API (SportsData.io)  
- **Programming Language:** Python 3.x  

### IAM Security  
- Least privilege policies for Lambda, SNS, and EventBridge.  

---

## Project Structure  
```plaintext
game-day-notifications/  
├── src/  
│   ├── gd_notifications.py         # Main Lambda function code  
├── policies/  
│   ├── gd_sns_policy.json          # SNS publishing permissions  
│   ├── gd_eventbridge_policy.json  # EventBridge to Lambda permissions  
│   └── gd_lambda_policy.json       # Lambda execution role permissions  
├── .gitignore  
└── README.md                       # Project documentation  

Setup Instructions
Clone the Repository

git clone https://github.com/ifeanyiro9/game-day-notifications.git  
cd game-day-notifications  

Create an SNS Topic

    Open the AWS Management Console.
    Navigate to the SNS service.
    Click Create Topic and select Standard as the topic type.
    Name the topic (e.g., gd_topic) and note the ARN.
    Click Create Topic.

Add Subscriptions to the SNS Topic

    Open the topic details.
    Go to the Subscriptions tab and click Create subscription.
    Choose a protocol:
        Email: Enter a valid email address and confirm the subscription via the email link.
        SMS: Enter a valid phone number in international format (e.g., +1234567890).
    Click Create Subscription.

Create the SNS Publish Policy

    Open the IAM service in the AWS Management Console.
    Navigate to Policies → Create Policy → JSON.
    Paste the JSON content from policies/gd_sns_policy.json, replacing REGION and ACCOUNT_ID with your AWS region and account ID.
    Review and create the policy.

Create an IAM Role for Lambda

    Open the IAM service and create a new role.
    Attach the following policies:
        SNS Publish Policy (e.g., gd_sns_policy).
        AWSLambdaBasicExecutionRole (AWS-managed policy).
    Save the role ARN for later use.

Deploy the Lambda Function

    Open the Lambda service in the AWS Management Console.
    Create a new function:
        Runtime: Python 3.x
        Assign the IAM role created earlier.
    Copy the content of src/gd_notifications.py into the function code editor.
    Add the following environment variables:
        NBA_API_KEY: Your NBA API key.
        SNS_TOPIC_ARN: The ARN of the SNS topic created earlier.
    Save the function.

Set Up Automation with EventBridge

    Open the EventBridge service.
    Create a new rule with the following settings:
        Event Source: Schedule.
        Cron Expression: Specify the desired schedule (e.g., hourly).
        Target: The Lambda function (e.g., gd_notifications).

Test the System

    Open the Lambda function in the AWS Management Console.
    Create a test event and run the function.
    Check CloudWatch Logs for any errors.
    Verify that SMS/Email notifications are received.

What We Learned

    Designing a notification system with AWS SNS and Lambda.
    Securing AWS services using least privilege IAM policies.
    Automating workflows with Amazon EventBridge.
    Integrating external APIs into cloud-based workflows.

