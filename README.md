
```bash
chmod +x *.sh

```

```bash
mkdir -p ~/.aws/

```

```
touch ~/.aws/credentials_multiclouddeploy

```

```
./aws_set_credentials.sh key.csv

```

```
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)

```

```
gcloud config set project $GOOGLE_CLOUD_PROJECT_ID

```

Execute the commands below to prepare the AWS and GCP environment

```bash
mkdir -p ~/.aws/
```
​
```bash
touch ~/.aws/credentials_multiclouddeploy
```
​
```bash
./aws_set_credentials.sh key.csv
```
​
```bash
GOOGLE_CLOUD_PROJECT_ID=$(gcloud config get-value project)
```
​
```bash
gcloud config set project $GOOGLE_CLOUD_PROJECT_ID
./gcp_set_project.sh
```

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
​
```bash
terraform init
```
​
```bash
terraform plan
```
​
terraform apply
