# Build a Real-Time Asset Tracking Application with Amazon Location Service

# Step 1: Install The Application
git clone https://github.com/aws-solutions-library-samples/guidance-for-tracking-assets-and-locating-devices-using-aws-iot.git --recurse-submodules

cd guidance-for-tracking-assets-and-locating-devices-using-aws-iot/

cd amazon-location-samples-react/tracking-data-streaming && npm install

chmod +x deploy_cloudformation.sh && export AWS_REGION=<your region> && ./deploy_cloudformation.sh  
     # Replace <your region> with the region where to deploy the App

# Step 2: Configure IoT Resources
## -> Go to guidance-for-tracking-assets-and-locating-devices-using-aws-iot/cf
aws cloudformation create-stack --stack-name TrackingAndGeofencingIoTResources --template-body file://iotResources.yml --capabilities CAPABILITY_IAM

## -> Get the status of the stack deployment
aws cloudformation describe-stacks --stack-name TrackingAndGeofencingIoTResources

# Step 3: Configure Visualization
## -> Go to guidance-for-tracking-assets-and-locating-devices-using-aws-iot/amazon-location-samples-react/tracking-data-streaming/src
aws cloudformation describe-stacks --stack-name TrackingAndGeofencingSample --query "Stacks[0].Outputs[*].[OutputKey, OutputValue]"

# => Set the values in configuration.js file

# Step 4: Preview running Application
## Go to guidance-for-tracking-assets-and-locating-devices-using-aws-iot/amazon-location-samples-react/tracking-data-streaming
npm start

# Step 5: View IoT Positions on the Map
# Go to AWS IoT Core -> MGTT test client -> Publish to a topic tab (location)
# Use the code for the Message payload -> set timestamp to current Epoch time.

{
  "payload": {
    "deviceid": "Vehicle-1",
    "timestamp": <Epoch Time>,
    "location": { "lat": 47.54372304079714, "long": -122.32275832917712 },
    "accuracy": { "Horizontal": 20.5 }
  }
}

# Publish

# Step 6: Host Application to CloudFront
# 6.(a). Create Bucket
# 6.(b). Build and upload Application files
## Go to guidance-for-tracking-assets-and-locating-devices-using-aws-iot/amazon-location-samples-react/tracking-data-streaming
npm run build
## 6.(c). Go to guidance-for-tracking-assets-and-locating-devices-using-aws-iot/amazon-location-samples-react/tracking-data-streaming/build
aws s3 cp . s3://<BucketName>/ --recursive  # Use the correct Bucket name

# Step 7: Deploy CloudFront Distribution
# Go to CloudFront -> Create distribution
# For Origin doman, select the newly created s3 bucket
# For Origin access, use "Origin access control settings (recommended)"
# Create new OCA -> Create

# Step 8: View Application via CloudFront
## Go to guidance-for-asset-tracking-using-aws-iot-core-and-amazon-location-services/amazon-location-samples-react/tracking-data-streaming
## -> Go to Start your App using the npm start command
## -> Go to CloudFront dashboard -> Details -> Distribution domain name
## -> Copy and paste it in your web browser -> add /index.html at the end 

# Step 9: Clean Up
## -> Detele CloudFormation stacks
## -> Delete S3 Bucket
## -> Disable CloudFront Distribution
## -> Stop the Application by using the letter "q"
