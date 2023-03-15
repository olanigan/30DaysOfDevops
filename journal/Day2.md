## Day 2: 

### Configure backend for terraform state

* Create Object storage in Linode and generate Access & Secret keys
* Create `backend` file and add to `.gitignore`

```
skip_credentials_validation = true
skip_region_validation = true
bucket="your-bucket"
key="your-terraform.tfstate"
region="us-east-1"
endpoint="us-east-1.linodeobjects.com"
access_key="access_key"
secret_key="secret_key"
```

* Add backend to `main.tf` in `terraform` block

```
backend "s3" {
        skip_credentials_validation = true
        skip_region_validation = true
}
```

* Initialize configured backend

<img width="563" alt="image" src="https://user-images.githubusercontent.com/2639639/225198019-144a5238-87d8-414b-89de-a767aa9ca84f.png">


### Install Docker on Linode instance

* Add provisioner in `linode-instance` definition
```
provisioner "remote-exec" {
        connection {
            host = "${self.ip_address}"
            type = "ssh"
            user = "root"
            password = "${var.root_user_pw}"
        }

        inline = [
            "sudo apt-get update",
            "curl -fsSL https://get.docker.com -o get-docker.sh",
            "sudo sh get-docker.sh"
        ]
    }
```
* Run `terraform apply -auto-approve`
* Login to Shell and validate Docker installation with `docker ps`

