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

## Installation and Deployment

### 1. Clone the Repository
```bash
git clone https://github.com/aws-solutions-library-samples/guidance-for-tracking-assets-and-locating-devices-using-aws-iot.git --recurse-submodules
cd guidance-for-tracking-assets-and-locating-devices-using-aws-iot

### 2. Install Dependencies and Deploy CloudFormation
cd amazon-location-samples-react/tracking-data-streaming
npm install
chmod +x deploy_cloudformation.sh
export AWS_REGION=<your-region>  # Replace with your AWS region
./deploy_cloudformation.sh

### 3. Configure IoT Resources
cd ../../cf
aws cloudformation create-stack --stack-name TrackingAndGeofencingIoTResources --template-body file://iotResources.yml --capabilities CAPABILITY_IAM
aws cloudformation describe-stacks --stack-name TrackingAndGeofencingIoTResources
