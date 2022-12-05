# Magic Lambda API - AWS Amplify Sample Project

This is an AWS Amplify project sample to create a Python Lambda named Magic with an API, deploy it to a live environment, test it and destroy the resources after using them.

## Prerequisites

1. Git installed on your computer: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
2. GitHub account created and able to work with remote repositories on GitHub: https://docs.github.com/en/get-started/quickstart/set-up-git
3. AWS Account - AWS CLI and AWS Amplify Installed on your computer: https://docs.amplify.aws/cli/start/install
4. Python and Pyenv installed: https://github.com/pyenv/pyenv
5. Time and snacks

## Steps

### Create a project on GitHub

Follow the steps on the GitHub Documentation on how to create a GitHub repository: https://docs.github.com/en/get-started/quickstart/create-a-repo

### Clone repository localy

```bash
git clone $USER/$PROJECT_NAME
```

### Create the first branch with the first commit with a README file

After cloning the repository, create a `README.md`, commit and push the commit into a new branch

```bash
touch README.md
git add README.md
git commit -m "Initial commit"
git push -u origin HEAD
```

Windows-based OS can use `type nul > README.md` instead of `touch README.md`

### Amplify Configure

The Amplify Configuration can be used by multiple projects under the same AWS account.

Follow the steps below for guidance on how to set up Amplify.

```bash
amplify configure
Specify the AWS Region
? region: eu-west-2
Specify the username of the new IAM user:
? user name: amplify-juancarlosjr97 # Enter your AWS profile to be used by Amplify Select your name
Complete the user creation using the AWS console # Follow the steps in the AWS console
Enter the access key of the newly created user:
? accessKeyId: ********\*\*\*\*********
? secretAccessKey: ******************\*\*\*\*******************
This would update/create the AWS Profile in your local machine
? Profile Name: amplify-juancarlosjr97 # Enter your AWS profile locally to be used by Amplify - Suggestion to match the one created in a previous step
```

After the setup has been successful the message should appear `Successfully set up the new user.`, otherwise start over.

### Amplify Init

From the root of your project locally, start a new amplify project following the steps below:

```bash
amplify init
Note: It is recommended to run this command from the root of your app directory
? Enter a name for the project magiclambda
The following configuration will be applied:

Project information
| Name: magiclambda
| Environment: dev
| Default editor: Visual Studio Code
| App type: javascript
| Javascript framework: none
| Source Directory Path: src
| Distribution Directory Path: dist
| Build Command: npm run-script build
| Start Command: npm run-script start

? Initialize the project with the above configuration? Yes
Using default provider awscloudformation
? Select the authentication method you want to use: AWS profile

For more information on AWS Profiles, see:
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html

? Please choose the profile you want to use amplify-juancarlosjr97 # Select the AWS profile created in a previous step
Adding backend environment dev to AWS Amplify app: magiclambdaapi
```

AWS Amplify will start creating the project in AWS and after it has finished it will show a message below:

```bash
Deployment completed.

✔ Help improve Amplify CLI by sharing non sensitive configurations on failures (y/N) · Yes # Optional - I always select yes to help the AWS Amplify team
Deployment bucket fetched.
✔ Initialized provider successfully.
✅ Initialized your environment successfully.

Your project has been successfully initialized and connected to the cloud!
```

### Creating Python Lambda

After a project has been created successfully, we can start working on it by adding a new Lambda using the steps below:

```bash
amplify add api
? Select from one of the below mentioned services: REST
✔ Provide a friendly name for your resource to be used as a label for this category in the project: · magicapi
✔ Provide a path (e.g., /book/{isbn}): · /
Only one option for [Choose a Lambda source]. Selecting [Create a new Lambda function].
? Provide an AWS Lambda function name: magiclambda
? Choose the runtime that you want to use: Python
Only one template found - using Hello World by default.

? Do you want to configure advanced settings? No
? Do you want to edit the local lambda function now? No
Successfully added resource magiclambda locally.
```

After the Lambda has been initialized, it will show the message below:

```bash
✅ Succesfully added the Lambda function locally
✔ Restrict API access? (Y/n) · No
✔ Do you want to add another path? (y/N) · No
✅ Successfully added resource magicapi locally
```

After the lambda has been created and before doing any modification, run `amplify push -y` that will create the resources in AWS, and at the end of the execution it will return the Endpoint to execute the lambda.

### Testing Python Lambda

```bash
curl $LAMBDA_ENDPOINT
```

#### Update and Test Lambda

Update the lambda `index.py` with any change and push the changes to AWS by typing `amplify push -y`.

### Create AWS Budget

Follow the tutorial created by AWS on how to create a budget for an AWS account: https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html

Budgets are important to control expenses within an account.

### Destroy Resources

To avoid continuing expending money, destroy the resources created using the amplify CLI or from the AWS Console using the Amplify dashboard using this guide https://aws.amazon.com/premiumsupport/knowledge-center/amplify-delete-application/

```bash
amplify delete
```

### Save your changes

Commit all your changes into your GitHub repository using

```bash
git add .
git commit -m "MEANINGFUL COMMIT MESSAGE"
git push
```
