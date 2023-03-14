## Day 1: Terraforming Linode

### Install Terraform

On MacOs, install Terraform with Brew
```
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

Confirm installation on new shell
```
terraform -version
```

### Import Sample Python Web App
```
git clone https://github.com/codingforentrepreneurs/iac-python
```

### Steps 

- Remove .git and re-initialized the project
- Add linode provider in main.tf and ran `terraform init`
- Generate Personal Access token in Linode and add to `terraform.tfvars`, make sure it's excluded from git
- Add SSH Key to `terraform.tfvars`. For MacOS, use `cat ~/.ssh/id_rsa.pub | pbcopy` to copy
- Generate `root_user_pw` with Python3 command: `python3 -c "import secrets;print(secrets.token_urlsafe(32))"`    
- Add token config for Linode provider and instance definition for `linode-instance`
- Run `terraform plan` and `terraform apply -auto-approve`
- Destroy resource with `terraform destory -auto-approve`
- Make changes to instance config and re-run plan, apply and destroy


### Screenshots



<img width="545" alt="image" src="https://user-images.githubusercontent.com/2639639/225081527-59381b94-8abf-4ad2-aee7-14396694ae4c.png">

![image](https://user-images.githubusercontent.com/2639639/225081627-5221d4f9-997f-4fb9-b4b2-642c30eee8d2.png)

<img width="580" alt="image" src="https://user-images.githubusercontent.com/2639639/225082381-aa84a382-77df-4066-a466-9b2b2e37984a.png">




