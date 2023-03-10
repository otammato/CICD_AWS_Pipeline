# CICD_AWS_Pipeline
create a CI/CD pipeline with AWS CodePipeline
<br><br>

CI/CD refers to the practice of continuously integrating and continuously deploying code. Creating a pipeline streamlines the process of releasing new software versions by automating tasks such as building the code, running tests, and deploying it securely. In this instance, We will be utilizing Github for the source code and an S3 bucket for the final deployment stage.
<br><br>
#### Prerequisites:
- AWS account
- Github account
<br><br>

### Step 1
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

Scroll all the way down to Static website hosting. Click on Edit and Enable static website hosting. Then type in <i>index.html</i> and <i>error.html</i> as indicated and click Save. Now move over to the Permissions tab. Here we will add a bucket policy to allow public read access. Click on the Edit bucket policy and input the JSON code below.

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
}</pre>

<br><br>
Don't forget to change the ARN to your bucket with ???/*??? after the ARN. Click Save. Your bucket is now publicly accessible.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_3.webp" width="700px"/>
</p>
<br><br>

### Step 2
Go to AWS CodePipeline and create a new pipeline. Give it a name and proceed. On the next page, select the option to add a source stage and choose GitHub (Version 2) as the source. Connect to your GitHub account by entering your username and password when prompted.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_4.png" width="700px"/>
</p>
<br><br>

Authorize the connector. Afterwards, you will be asked to specify which repositories AWS can access. Select the appropriate repository and click on the Install > Connect button. You will be directed back to CodePipeline. Now, select your repository and specify the branch name.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_5.png" width="700px"/>
</p>
<br><br>

### Step 3
Next, you are asked to choose a builder, indicate AWS CodeBuild. Choose your Region and click create a project, this will bring you to CodeBuild. In CodeBuild we use the following configurations:
<br>
- Managed Image
- Amazon Linux 2
- Standard runtime
- aws/codebuild/amazonlinux2-x86_64-standard:4.0
- Always use the latest image for this runtime version
- Linux
- Create a New Service Role
<br>
Then click on Continue to CodePipeline. Back in CodePipeline, you should find that your project was successfully built in CodeBuild.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_6.webp" width="700px"/>
</p>
<br><br>

### Step 4
The deploy stage! We will be deploying to the S3 bucket you just created. Choose S3 and your bucket.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_7.webp" width="700px"/>
</p>
<br><br>

Click Next to review the stages and if it all looks good then click on Create pipeline. When it is done deploying your screen should look like this.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_8.webp" width="700px"/>
</p>
<br><br>

Now that the code is deployed to S3 we can check by grabbing the S3 website endpoint. Found in the properties tab of your S3 bucket, scroll all the way to the bottom of the page.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_9.webp" width="700px"/>
</p>
<br><br>

Copy and paste the URL in your browser???
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_10.webp" width="700px"/>
</p>
<br><br>

And here is our static website! That we are able to view due to the read permissions given to the public.
<br><br>

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_11.webp" width="700px"/>
</p>
<br><br>

### Step 5
To verify that the Code Pipeline is triggered I will make a change to the code in GitHub. The pipeline should automatically trigger and make the changes. Let???s test it out! I will edit the HTML file and commit the changes.
<br><br>

```
<p>Hello World</p>
<p>Hello World</p>
```
<br><br>

Checking on the Pipeline back in the AWS console you can actually see the Pipeline at work. It is automatically taking in the changes and executing them.
<br><br>


<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_12.webp" width="700px"/>
</p>
<br><br>

<br><br>
When refreshing the static website the changes I made to the file should appear.

<p align="center" >
  <img src="https://github.com/otammato/CICD_AWS_Pipeline/blob/main/images/image_13.webp" width="700px"/>
</p>
<br><br>

