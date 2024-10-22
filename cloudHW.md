# Домашнее задание к занятию "`Отказоустойчивость в облаке`" - `Османов Ренат`


### Задание 1

Токен был удален для безопасности(а json ключ я не смог создать)

````
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
  required_version = ">= 1.3.0"
}
provider "yandex" {
  token                    = ""
  cloud_id                 = "b********************v"                     
  folder_id                = "b1goa*****************"                             
  zone                     = "ru-central1-a"                             
}

resource "yandex_compute_instance" "vm" {
  count = 2
  name = "vm${count.index + 1}"
  resources {
    cores         = 2
    memory        = 2
    core_fraction = 5
  }
  boot_disk {
    initialize_params {
      image_id = "fd82vol772l2nq9p12pb"
      size     = 5
    }
  }
  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }
 metadata = {
  user-data = <<-EOF
    #!/bin/bash
    apt update
    apt install -y nginx
    systemctl start nginx
    systemctl enable nginx
  EOF

  ssh-keys = "ubuntu:${file("//Users/rcz/.ssh/netology1.pub")}"  # ваш публичный ключ
}
}
resource "yandex_vpc_network" "network-1" {
  name = "network1"
}
resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-a"
  network_id     = yandex_vpc_network.network-1.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

resource "yandex_lb_network_load_balancer" "balancer" {
  name = "balancer"
  listener {
    name = "listener"
    port = 80
    external_address_spec {
      ip_version = "ipv4"
    }
  }
  attached_target_group {
    target_group_id = "${yandex_lb_target_group.target.id}"
    healthcheck {
      name = "http"
        http_options {
          port = 80
          path = "/"
        }
    }
  }
}


resource "yandex_lb_target_group" "target" {
  name      = "target-group"

  dynamic "target" {
    for_each = "${yandex_compute_instance.vm[*].network_interface.0.ip_address}"
    content {
      subnet_id = "${yandex_vpc_subnet.subnet-1.id}"
      address   = target.value
    }
  }
}

````




balancer

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/cloudFF/cloud1.1.png)


NGINX

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/cloudFF/cloud1.2.png)





