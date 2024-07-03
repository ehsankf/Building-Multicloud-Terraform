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
