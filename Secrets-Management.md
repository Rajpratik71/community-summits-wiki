## Secrets Management with Chef
Current Best Practice/Model is to use [HashiCorp Vault](https://www.vaultproject.io/)

Other Options/Ideas:
* [Chef Vault](https://docs.chef.io/chef_vault.html) - Created by Nordstrom has problems searching
* AWS [Parameter Store](https://aws.amazon.com/ec2/systems-manager/parameter-store/) & [KMS](https://aws.amazon.com/kms/) - 
* AWS [S3](https://aws.amazon.com/s3/) - 
* [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/Q) - 
* [EnvKey](https://www.envkey.com/) - 
* gpg encrypted secrets - 
* [BLESS](https://github.com/Netflix/bless) (Bastion's Lambda Ephemeral SSH Service) - Promising release from Netflix (AWS Only)
* [SSH Certificate Authority](https://github.com/cloudtools/ssh-cert-authority) - 
* LDAP - for secrets/ssh keys
* Travso? 
* SOPS? 


Misc. Notes:

Chef nodes can sometimes lie about current setup/settings. -- This was mentioned when asking how to see what Nodes are using what data-bags/keys etc. 



