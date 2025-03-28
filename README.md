# AWS-SERVERLESS-WEB-APPLIATION

## Overview
This project is a **serverless** student management system that allows users to perform CRUD operations on student data using **AWS Lambda, API Gateway, DynamoDB, S3, and CloudFront**. The system is designed to be fully managed, scalable, and cost-efficient, eliminating the need for traditional servers.

## Architecture
The project follows a **serverless architecture** using AWS services:
1. **Amazon API Gateway** – Handles HTTP requests and routes them to Lambda.
2. **AWS Lambda** – Processes business logic for inserting and retrieving student data.
3. **Amazon DynamoDB** – A NoSQL database used to store student records.
4. **Amazon S3** – Hosts the static frontend files (HTML, CSS, JavaScript).
5. **Amazon CloudFront** – Serves the frontend securely via a global CDN with HTTPS support.

## Tech Stack
- **Frontend**: HTML, CSS, JavaScript (hosted on S3)
- **Backend**: Python (AWS Lambda)
- **Database**: Amazon DynamoDB (NoSQL)
- **API Management**: Amazon API Gateway
- **Security & Performance**: CloudFront (CDN), IAM (Permissions)

## Features
✅ **Serverless & Fully Managed** – No need for provisioning or maintaining servers.
✅ **RESTful API** – Supports CRUD operations via API Gateway.
✅ **Scalable & Cost-Effective** – AWS handles scaling, security, and performance.
✅ **Secure Static Hosting** – Frontend hosted on S3 and delivered via CloudFront.

## Setup & Deployment
### Prerequisites
- AWS account
- AWS CLI configured with appropriate IAM permissions
- Python 3.x and Boto3 installed

### Steps
1. **Create an S3 Bucket** for hosting frontend files.
2. **Upload Static Files** (HTML, CSS, JS) to S3.
3. **Set up a DynamoDB table** (`studentData`) with the required schema.
4. **Deploy AWS Lambda functions** using Python and Boto3.
5. **Configure API Gateway** to trigger Lambda functions.
6. **Deploy CloudFront** for secure, fast content delivery.
7. **Test API Endpoints** using Postman or Curl.

## API Endpoints
| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | `/students` | Retrieve all student records |
| POST | `/students` | Add a new student record |

## Sample Lambda Code
### **Retrieve Students from DynamoDB**
```python
import json
import boto3

def lambda_handler(event, context):
    dynamodb = boto3.resource('dynamodb', region_name='us-east-2')
    table = dynamodb.Table('studentData')
    response = table.scan()
    return {
        'statusCode': 200,
        'body': json.dumps(response['Items'])
    }
```

### **Insert Student into DynamoDB**
```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('studentData')

def lambda_handler(event, context):
    student_id = event['studentid']
    name = event['name']
    student_class = event['class']
    age = event['age']
    
    table.put_item(Item={
        'studentid': student_id,
        'name': name,
        'class': student_class,
        'age': age
    })
    
    return {
        'statusCode': 200,
        'body': json.dumps('Student data saved successfully!')
    }
```

## Security Measures
- IAM roles restrict API and database access.
- CloudFront enforces HTTPS and caching for performance.
- API Gateway enforces rate limits and authentication (optional).

## Future Enhancements
- Implement **user authentication** using Amazon Cognito.
- Add a **frontend UI** with React.js for better interaction.
- Enhance **monitoring and logging** using AWS CloudWatch.

## Conclusion
This **serverless student management system** demonstrates how AWS services can be used to build a scalable and secure application. By leveraging API Gateway, Lambda, DynamoDB, S3, and CloudFront, the system is **cost-efficient, highly available, and easy to maintain**. 🚀

