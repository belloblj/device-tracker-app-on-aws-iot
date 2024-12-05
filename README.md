# Real-Time Asset Tracking Application with AWS IoT and Amazon Location Service

This project demonstrates how to build a real-time asset tracking application using AWS IoT, Amazon Location Service, CloudFormation, and CloudFront. It provides end-to-end guidance on deploying IoT resources, configuring the frontend, and hosting the application.

## Features
- **Real-time tracking**: Monitor device locations in real-time.
- **AWS IoT integration**: Utilize AWS IoT Core to manage and publish location data.
- **CloudFront hosting**: Deploy the frontend via AWS CloudFront for global access.
- **Visualization**: Display asset positions on an interactive map.

## Prerequisites
- AWS CLI installed and configured
- Node.js and npm installed
- AWS account with appropriate permissions

  https://community.aws/content/2i9a3mWGOdvjWY27qK2EJXvNxnu/build-a-real-time-asset-tracking-application-with-amazon-location-service

## Installation and Deployment

### 1. Clone the Repository
```bash
git clone https://github.com/aws-solutions-library-samples/guidance-for-tracking-assets-and-locating-devices-using-aws-iot.git --recurse-submodules
cd guidance-for-tracking-assets-and-locating-devices-using-aws-iot
```
### 2. Install Dependencies and Deploy CloudFormation
```bash
cd amazon-location-samples-react/tracking-data-streaming
npm install
chmod +x deploy_cloudformation.sh
export AWS_REGION=<your-region>  # Replace with your AWS region
./deploy_cloudformation.sh
```

### 3. Configure IoT Resources
```bash
cd ../../cf
aws cloudformation create-stack --stack-name TrackingAndGeofencingIoTResources --template-body file://iotResources.yml --capabilities CAPABILITY_IAM
aws cloudformation describe-stacks --stack-name TrackingAndGeofencingIoTResources
```

### 4. Configure Visualization
```bash
cd ../amazon-location-samples-react/tracking-data-streaming/src
aws cloudformation describe-stacks --stack-name TrackingAndGeofencingSample --query "Stacks[0].Outputs[*].[OutputKey, OutputValue]"
# Update the configuration.js file with the output values
```

### 5. Start the Application Locally
```bash
cd ..
npm start
```

### 6. Build and Host the Application
```bash
npm run build
cd build
aws s3 cp . s3://<BucketName>/ --recursive  # Replace <BucketName> with your S3 bucket name
```

### 7. Deploy CloudFront Distribution
Create a CloudFront distribution from the AWS Console using the S3 bucket as the origin and configure Origin Access Control.

### 8. Access the Application
Copy the CloudFront Distribution Domain Name and open the URL in your browser, appending /index.html


### 9. Cleanup
```bash
aws cloudformation delete-stack --stack-name TrackingAndGeofencingIoTResources
aws cloudformation delete-stack --stack-name TrackingAndGeofencingSample
# Manually delete S3 bucket and disable CloudFront distribution
```

## License
This project is licensed under the MIT License. See LICENSE for more details.

### Highlights:
- Clear structure with steps for cloning, installing, and deploying.
- Includes necessary AWS CLI commands.
- Sections for features, prerequisites, and cleanup for clarity.


