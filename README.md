#### Setting up AWS and GCP environemnt
Execute the commands below to prepare the AWS and GCP environment
```bash
chmod +x *.sh
```
```bash
mkdir -p ~/.aws/
```
```
touch ~/.aws/credentials_multiclouddeploy
```
Creating the Access Key for the terraform-en-1 user using the IAM service and rename it as `key.csv` and upload it to GCP

```
./aws_set_credentials.sh key.csv
```
```
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)
```
```
gcloud config set project $GOOGLE_CLOUD_PROJECT_ID
```

```bash
mkdir -p ~/.aws/
```
```bash
touch ~/.aws/credentials_multiclouddeploy
```
```bash
./aws_set_credentials.sh key.csv
```
```bash
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)
```

#### Setting up the GC Shell
Execute the command below to set the project in the Google Cloud Shell
```bash
gcloud config set project $GOOGLE_CLOUD_PROJECT_ID
./gcp_set_project.sh
```

#### Setting up the GC APIs
Execute the commands to enable the Kubernetes, Container Registry, and Cloud SQL APIs
```bash
gcloud services enable containerregistry.googleapis.com
```
```
gcloud services enable container.googleapis.com
```
```
gcloud services enable sqladmin.googleapis.com
```
```
gcloud services enable cloudresourcemanager.googleapis.com
```
```
gcloud services enable serviceusage.googleapis.com
```
```
gcloud services enable compute.googleapis.com
```
```
gcloud services enable servicenetworking.googleapis.com --project=$GOOGLE_CLOUD_PROJECT_ID
```

#### Running Terraform to provision MultiCloud infrastructure in AWS and Google Cloud
Execute the following commands to provision infrastructure resources

```bash
cd ~/mission1/en/terraform/
```
```bash
terraform init
```
```bash
terraform plan
```
```bash
terraform apply
```
#### Connect to MySQL DB running on Cloud SQL 
```
mysql --host=**<replace_with_public_ip_cloudsql>** --port=3306 -u app -p
```
Once you're connected to the database instance, create the products table for testing purposes
```
use dbcovidtesting;
```
```
source ~/application/db/create_table.sql
```
```
show tables;
```
```
exit;
```
Enable Cloud Build API via Cloud Shell.
```
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)
```
```
cd application/app
```
```
gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT_ID/luxxy-covid-testing-system-app-en
```
#### Build the Docker image and push it to Google Container Registry
```
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)
```
```
cd application/app
```
```
gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT_ID/luxxy-covid-testing-system-app-en
```
#### Deploy application on GKE (Google Kubernetes Engine) cluster 
Open the Cloud Editor and edit the Kubernetes deployment file `(*.yaml)` and update the variables with your 
- <PROJECT_ID> on the Google Container Registry path
- AWS Bucket name, AWS Keys (open file access key cvs file and use Access key ID and Secret access key)  
- Cloud SQL Database Private IP.

```bash
cd application/kubernetes/
luxxy-covid-testing-system.yaml

				image: gcr.io/<PROJECT_ID>/luxxy-covid-testing-system-app-en:latest

				- name: AWS_BUCKET
          value: "luxxy-covid-testing-system-pdf-en-xxxx"
        - name: S3_ACCESS_KEY
          value: "xxxxxxxxxxxxxxxxxxxxx"
        - name: S3_SECRET_ACCESS_KEY
          value: "xxxxxxxxxxxxxxxxxxxx"
        - name: DB_HOST_NAME
          value: "xxxxxxxx"
```

Connect to the GKE (Google Kubernetes Engine) cluster via Console

Deploy the application Luxxy in the Cluster
```
cd application/kubernetes
```
```
kubectl apply -f *.yaml
```

