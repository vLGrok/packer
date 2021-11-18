# Packer

Upgrading legacy JSON

Given the old JSON variables file:

```json
{
  "variables": {
    "aws_region": null,
    "aws_secondary_region": "{{ env `AWS_DEFAULT_REGION` }}",
    "aws_secret_key": "",
    "aws_access_key": ""
  },
  "sensitive-variables": ["aws_secret_key", "aws_access_key"]
}
```

Calling the hcl2_upgrade command:

```bash
packer hcl2_upgrade variables.json
```

Produces the file variables.pkr.hcl:

```hcl2
variable "aws_access_key" {
  type      = string
  default   = ""
  sensitive = true
}

variable "aws_region" {
  type = string
}

variable "aws_secondary_region" {
  type    = string
  default = "${env("AWS_DEFAULT_REGION")}"
}

variable "aws_secret_key" {
  type      = string
  default   = ""
  sensitive = true
}
```
