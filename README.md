# packer

# Files Content:
- jenkins_server.sh: Script to install Jenkins Server
- template.json: Template to create a VM image
- variables.json: Definition of the variables that we call from template.json file

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
packer build -var-file=variables.json template.json
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


- Using the variables file to install jenkins script:
```sh
{
"variables": {
        "service_account_json": "~/shared/iliasproject-214108-fe834ddf82b4.json",
        "repo_path": "~/packer_dir/",
        "project_id": "iliasproject-214108"
},

"builders": [
    {
      "type": "googlecompute",
      "account_file": "iliasproject-214108-fe834ddf82b4.json",
      "project_id": "iliasproject-214108",
      "source_image_family": "{{user `source_image_family`}}",
      "ssh_username": "{{user `ssh_username`}}",
      "zone": "us-central1-a"
    }
  ],

"provisioners": [
        {
                "type": "shell",
                "script": "jenkins_server.sh",
                "pause_before": "05s"
        }
]
}
```
