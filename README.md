# Contact_Form


## Building a Contact Form with Lambda, API Gateway and SES
This lesson demonstrates a web page with a typical contact form. Using API Gateway and a Lambda function as a backend for this form, we will send the form post contents via email using SES, and also write the contact data to DynamoDB.

### Architecture Workflow

```
1. DynamoDB
Create table Contact with primary partition key id

2. Lambda function
Create function ContactEmail
Add the following Environment Variables:

  Key                    Value
- [DYNAMODB_TABLE]	 [name of the dynamodDB table]
- [SENDER_EMAIL]	 [your email]

3. IAM role
Create IAM role with a policy to allow for email send, put to dynamoDB and CloudWatch logs.

4. API Gateway
- Create API ContactEmailAPI
- Create Method
- Integration Type: Lambda Function
- Use Lambda Proxy Integration: Checked (stores request data in event)
- Lambda region: Same region as Lambda function
- Lambda function: ContactEmail
- Enable CORS
- Select the POST method
- Under Actions select Enable CORS
- Leave the default options and click on Enable CORS and replace existing CORS headers.
- Click Yes, replace existing values
- Deploy API
- Under Actions select Deploy API
- Deployment stage: [New stage]
- Stage name: dev

5. Finally, capture the API Invoke URL and update the form.js.
```



### Test locally:

```
cd Contact_Form
python3 -m http.server
```

Browse http://localhost:8000

