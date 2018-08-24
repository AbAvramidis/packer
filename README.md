# packer

# Download  & Install Packer

| Download page | [https://www.packer.io/downloads.html]

- Create a bash script:

```sh
#!/bin/bash
remote_zip="https://releases.hashicorp.com/packer/1.2.5/packer_1.2.5_linux_amd64.zip"
local_zip="/tmp/packer.zip"
wget "${remote_zip}" -O "${local_zip}"
sudo unzip $local_zip -d /opt/packer/
sudo ln -s /opt/packer/packer /usr/bin/packer
```

# Packer commands & Configuration file

```sh
packer version
packer validate file.json
packer build

```
| Web resources | [https://medium.com/the-andela-way/building-custom-machine-images-with-packer-a21c6d932bf6
https://www.packer.io/docs/builders/googlecompute.html
https://www.davidbegin.com/a-packer-terraform-structure/]


- Packer Configuration .json file example:

```sh

{
"builders": [
	{
	"type": "googlecompute"
	"account_file": "/home/vagrant/.....json",
	"project_id": "gcp-projectid",
	"source_image_family": "centos-7",
	"ssh_username": "packer",
	"zone": "europe-west2-a",
	"image_name": ""
	}
],

"provisioners": [
	{
	"type": "shell",
	"inline": "sudo yum update -y"
	}
]
}

```


- Run packer image through terraform 
image = "packer-1535104174" int Variables folder
