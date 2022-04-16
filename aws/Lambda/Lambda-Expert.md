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

## Use Case 1 :

