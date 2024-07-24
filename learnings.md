# Terraform learnings

Sample dynamic block inside a resource in Terraform.


```hcl
dynamic "taints" {
    for_each = each.value.taints
    content {
        effect = taints.value.effect
        key    = taints.value.key
        value  = taints.value.value
    }
}
```

o/p

```
taints{
    effect = abc
    key = abc
    value = abc
}
```


Choosing a list based on env

```hcl
azs = {
    dev = ["us-east-1a","us-east-1b"],
    prod = ["us-east-1a", "us-east-1b"],
}[var.env]
```

## Some weird bug in terraform when using Azure provider

- When creating a terraform module which has data source inside of the module results in an unexpected behaviour when terraform plan is run leading to data being refreshed instead of it being maintaned in Terraform statefile.
- The potential fix is to move out the data blocks inside the module to the calling module, then pass the data fetched as a variable.
