## Lambda Function-As-Service (FaaS) - Expert Use Cases
Lambda is a great technology choice for background processing that is triggered by events.

Typical use cases of AWS Lambda include:

- Image transformation for newly uploaded images.
- Real-time metric data processing.
- Streaming data validation, filtering, and transformation.
- Lambda is very good at handling massive scale loads without the need to increase the amount of infrastructure.
- allocated to your application. Unlike Amazon EC2, which is priced by the hour but metered by the second, AWS Lambda is metered by rounding up to the nearest millisecond with no minimum execution time.
- It is important to note that serverless as an execution model is meant for workloads that are ephemeral and event-triggered. 
- Good serverless design principles state that one should assume that the environment exists only for a single invocation. If you are depending on data structures or temporary files to hold internal state between multiple invocations, serverless is not the right design choice.

## Use Case 1 : Operating serverless websites


This is one of the killer use cases to take advantage of the pricing model of Lambda and S3 hosted static websites.

Consider hosting the web frontend on S3 and accelerating content delivery with Cloudfront caching.

The web frontend can send requests to Lambda functions via API Gateway HTTPS endpoints. Lambda can handle the application logic and persist data to a fully-managed database service (RDS for relational, or DynamoDB for a non-relational database). 

You can host your Lambda functions and databases within a VPC to isolate them from other networks. As for Lambda, API Gateway and S3, you pay only after the traffic incurred, the only fixed cost will be running the database service.

## Use Case 2 : 