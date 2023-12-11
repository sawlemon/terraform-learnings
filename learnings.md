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