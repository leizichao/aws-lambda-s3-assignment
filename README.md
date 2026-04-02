# aws-lambda-s3-assignment

## Scenario
A Lambda function is triggered when a file is created in an S3 bucket.

---

## 1. Purpose of the Execution Role on the Lambda Function

The execution role defines what the Lambda function is allowed to do when it runs.

- It is assumed by AWS Lambda at runtime
- Grants permissions to access other AWS services
- Controls outbound actions

### Examples:
- Writing logs to CloudWatch Logs
- Reading from or writing to S3
- Accessing databases or other AWS services

**Summary:**
Execution role = permissions for Lambda to interact with AWS resources

---

## 2. Purpose of the Resource-Based Policy on the Lambda Function

The resource-based policy defines who or what is allowed to invoke the Lambda function.

- Attached directly to the Lambda function
- Controls inbound access
- Specifies trusted principals (e.g., AWS services)

### Example:
- Allowing S3 to trigger the Lambda function when a file is uploaded

**Summary:**
Resource-based policy = who can invoke the Lambda function

---

## 3. If the Lambda Function Needs to Upload a File into an S3 Bucket

### (a) Needed Update on the Execution Role

The execution role must be updated to allow the Lambda function to upload files to S3.

- Add permission to perform:
  - `s3:PutObject`
- Scope should follow least privilege:
  - Restrict to a specific bucket (and optionally a prefix)

**Summary:**
Update execution role to allow writing objects to S3

---

### (b) New Resource-Based Policy Needed?

No new resource-based policy is required.

**Reason:**
- The Lambda function is calling S3 (outbound action)
- Resource-based policies are only needed when another service invokes Lambda

In this case:
- S3 → Lambda trigger is already configured
- Lambda → S3 upload is controlled by the execution role

**Summary:**
No additional resource-based policy is needed

---

## Key Concept Summary

- Execution Role → What Lambda can do (outbound permissions)
- Resource-Based Policy → Who can invoke Lambda (inbound permissions)

---

## Services Referenced

- AWS Lambda
- Amazon S3
- Amazon CloudWatch Logs

