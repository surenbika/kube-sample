# This is a sample application stakc of a Apache webserver and mysql instance running on Kubernetes

## The resources are already provisioned, including file share of name testshare

## Get the secrets

Kubernetes needs credentials to access the file share we have created. These credentials are stored in a Kubernetes secret, which is referenced when you create a Kubernetes pod.

To create the secret:
Run following command with the correct account name and storage account key


STORAGE_KEY=$(az storage account keys list --resource-group azure-k8stest --account-name test --query "[0].value" -o tsv)

kubectl create secret generic azure-secret --from-literal=azurestorageaccountname=<...> --from-literal=azurestorageaccountkey=<...>

## Provision resource
1. Run $kubectl create -f weberver.yaml
This will provision webserver for you

2. Run $kubectl create -f webserver-svc.yaml

3. Provide mysql secrets by setting them as environment variables

4. Run $kubectl create -f mysql.yaml

5. Run $kubectl create -f mysql-svc.yaml

6. Connect to your MySQL DB and make connection string changes in the code
