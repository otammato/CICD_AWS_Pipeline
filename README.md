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

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_1.webp" width="700px"/>
</p>
<br><br>

After you click on 'Create bucket,' you will then set up the bucket to host a static website by navigating to the Properties tab within the bucket.

<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_2.webp" width="700px"/>
</p>
<br><br>

Scroll all the way down to Static website hosting. Click on Edit and Enable static website hosting. Then type in index.html and error.html as indicated and click Save. Now move over to the Permissions tab. Here we will add a bucket policy to allow public read access. Click on the Edit bucket policy and input the JSON code below.

<br>
<pre>
{
    "Version": "2012-10-17",
    "Id": "Policy1653853839796",
    "Statement": [
        {
            "Sid": "Stmt1653853838629",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::cicd-pipeline-deploy/*"
        }
    ]
}
</pre>
