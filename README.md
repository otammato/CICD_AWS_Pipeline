# CICD_AWS_Pipeline
create a CI/CD pipeline with AWS CodePipeline
<br><br>

CI/CD refers to the practice of continuously integrating and continuously deploying code. Creating a pipeline streamlines the process of releasing new software versions by automating tasks such as building the code, running tests, and deploying it securely. In this instance, We will be utilizing Github for the source code and an S3 bucket for the final deployment stage.
<br><br>
#### Prerequisites:
- AWS account
- Github account
<br><br>

#### Step 1
In the initial step, we will establish an S3 bucket to host a static website. To begin, go to the S3 section of the AWS console. Select Buckets and then click on Create bucket. Here, you will give the bucket a unique name, select the region, and ensure that the bucket is accessible to the public by disabling the option for "Block all public access.
<br><br>

<p align="center" width="200px">
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_1.webp" />
</p>
<br><br>

After you click on 'Create bucket,' you will then set up the bucket to host a static website by navigating to the Properties tab within the bucket.
