# corellium_v1project

## Example

```terraform
resource "corellium_v1project" "example" {
  name = "example"
  settings = {
    internet_access = false
    dhcp = false
  }
  quotas = {
    cores = 1
    instances = 2.5
    ram = 6144
  }
  users = []
  teams = [
    {
        id = "00000000-0000-4000-0000-000000000000"
        role = "admin"
    }
  ]
  keys = [
    {
      label = "example"
      kind  = "ssh"
      key   = "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKGWrBz0P8BWaELhsocREATc3jmhfyxFuADq07xdnZTz test"
    }
  ]
}
```

## Schema

### Required

- `name` (string) - The name of the project.

- `settings` (object of `settings`) - The settings of the project.

- `quotas` (object of `quotas`) - The quotas of the project.

- `users` (list of `user`) - The users associated to this project

- `teams` (list of `team`) - The teams associated to this project.

- `keys` (list of `key`) - The authorized keys associated to this project.

### Optional

### Read-only

- `id` (string) - Project ID.

- `created_at` (string) - Project creation time.

- `updated_at` (string) - Project update time.

### Nested schema for `settings`

#### Required

- `internet_access` (bool) - Whether the project has internet access.

- `dhcp` (bool) - Whether the project has DHCP.

### Nested schema for `quotas`

#### Required

- `cores` (number) - The number of cores.

#### Read-only

- `instances` (number) - The number of instances. Instances is computed as `cores * 2.5`.

- `ram` (number) - The amount of RAM in MB. Ram is computed as `cores * 6144`.

### Nested schema for `team`

#### Required

- `id` (string) - Team ID.

- `role` (string) - Team role on project. Must be "admin" or "\_member\_".

#### Read-only

- `label` (string) - Team label.

### Nested schema for `user`

#### Required

- `id` (string) - User ID.

- `role` (string) - User role on project. Must be "admin" or "\_member\_".

#### Read-only

- `name` (string) - User name.

- `label` (string) - User label.

- `email` (string) - User e-mail.

### Nested schema for `key`

#### Required

- `label` (string) - Key label.

- `kind` (string) - Key kind. Must be "ssh" or "agent".

- `key` (string) - Key content.

#### Read-only

- `id` (string) - Key ID.

- `fingerprint` (string) - Key fingerprint.

- `created_at` (string) - Key creation time.

- `updated_at` (string) - Key update time.
