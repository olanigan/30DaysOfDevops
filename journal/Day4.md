# Day 4: Using Provisioners to install Docker

Provisioned Linode with Docker install and replaced using Terraform inline provisioner with file provisioner

Provisioner configuration is added to the `linode-instance` definition inside `main.tf`:

### File Provisioner to copy script to instance
```
provisioner "file" {
    connection {
      host = "${self.ip_address}"
      type = "ssh"
      ...
    }
    
    source = "bootstrap-docker.sh"
    destination = "/tmp/bootstrap-docker.sh"
}
```

### Exec Provisioner to run script
```
provisioner "remote-exec" {
    connection {
      host = "${self.ip_address}"
      type = "ssh"
      ...
    }
    
    inline = [
        "chmod +x /tmp/bootstrap-docker.sh",
        "sudo sh /tmp/bootstrap-docker.sh",
        "mkdir -p /var/www/src/",
    ]
}
```

