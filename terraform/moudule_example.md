# terraform module example (nginx)

- main.tg

```
module "nginx" {
  source         = "./modules"
  container_name = "nginx_sample_container"
  external_port  = 8080
}
```

- modules/nginx.tf

```
variable "container_name" {
  description = "The name of the Docker container"
}

variable "external_port" {
  description = "external_port"
  type        = number
}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = var.container_name

  ports {
    internal = 81
    external = var.external_port
  }
}
```

- modules/provider.tf

```
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}
```
