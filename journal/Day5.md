# Day 5: More Provisioners to build and run Docker


## Using Terraform Locals

Create a new file `locals.tf` in the same directory as `main.tf` and add the following:

```
locals {
  root_dir = "${abspath(path.root)}"
  project_dir = "“${dirname(local.root_dir)}"
}
```

- `root_dir` refers to the Terraform working directory where the terraform files can be found
- `project_dir` refers to the Project directory for the application


## Copy Application source code 

```
provisioner "file" {
        connection {
            ...
        }

        source = "${local.project_dir}/src/"
        destination = "/var/www/src/"
    }

```

## Copy Dockerfile

```
provisioner "file" {
        connection {
            ...
        }

        source = "${local.project_dir}/src/"
        destination = "/var/www/src/"
    }

```

## Docker Build and Run 

**Use file provisioner to copy all other needed files**
```
provisioner "remote-exec" {
      connection {
        host = "${self.ip_address}"
        type = "ssh"
        user = "root"
        password = "${var.root_user_pw}"
      }

      inline = [
        "cd /var/www/",
        "docker build -t pyapp .",
        "docker run  --restart always -p 80:80 -d pyapp",
      ]
}
```
