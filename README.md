
# CrowdStrike - Google Cloud GKE POV
Use this terraform configuration to stand up a GCP environment including a Network, GKE Kubernetes Cluster and other supporting resources, to deploy and test CrowdStrike products such as the Falcon Operator, Falcon Sensors and Kubernetes Protection Agent.

## How to Deploy

  1. Clone this repo
  2. Review and modify gke-pov.tfvars with correct Provider Configuration 
  3. Review and modify addtional parameters in gke-pov.tfvars for further customization
  4. Run appropriate Terraform commands
  
```bash
terraform init
terraform plan -var-file="gke-pov.tfvars"
terraform apply -var-file="gke-pov.tfvars"
```

## How to use gke-pov.tfvars

The tfvars file allows you to quickly configure various parameters which are passed to the modules when terraform actions are executed.  This ensures your environment is customizable with optional resources, custom naming convention and other parameters without the need to modify code.  If you run the terraform commands without referencing the tfvars file in the -var-file argument, you will be prompted to enter values for several variables. 

### Parameter Details:

**Provider Configuration:** 
- credentials: (string) filename of you GCP Service Account Key
- project: (string) Your GCP Project ID
- region: (string) Your GCP Region
- zone: (string) Your GCP Zone
  
**Optional Features:** 
- autopilot: (bool) Whether to use GKE Autopilot Nodes (for more information, see: https://prometheus.io/docs/introduction/overview/)
- bastion: (bool) Whether to deploy a Bastion Instance with access to GKE Cluster
- prometheus: (bool) Whether to deploy a Prometheus Stack to your GKE Cluster for performance monitoring
- detection container: (bool) Whether to deploy the CrowdStrike Detection container to your GKE Cluster to easily generate detections for testing (for more information, see: https://github.com/CrowdStrike/detection-container)
  
**Infrastructure Configuration:** 
- alias: (string) Custom value to append to names of deployed resources
- subnet(s): (CIDR) CIDR Range for each subnet of the Network

**GKE Configuration:** 
- gke-num-nodes: (number) The number of GKE nodes per zone

## GCP Service Account Key

To manage you GCP Project workloads with Terrafom, you must reference a Service Account key in the Provider.  This key is set in the "credentials" parameter of the Provider Configuration in gke-pov.tfvars as described above.  

As a placeholder, this repo provides a GCP Service Account key template named my-gcp-key.json.  To successfully run this configuration, this file must be updated or replaced.  Please create and download your GCP Service Account Key, then proceed in one of two ways:

  1. Copy the contents of your new key file and paste it into my-gcp-key.json  

or  

  2. Save your new key file in the working directory of this terraform configuration.  Then in gke-pov.tfvars, update the credentials parameter with the new key file name

For more information on creating GCP Service Account keys please see the documentation: https://cloud.google.com/iam/docs/creating-managing-service-account-keys
