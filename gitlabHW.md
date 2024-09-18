# Домашнее задание к занятию "`8.3 GitLab`" - `Османов Ренат`


### Задание 1

![img](/img/gitlab1.2.png)
![img](/img/gitlab1.3.png)

### Задание 2


````
stages:
  - test
  - build

test:
  stage: test
  image: golang:1.17
  script:
   - go test .

build:
    stage: test
    image: docker:latest
    script:
        docker build .
````

![img](/img/gitlab2.3.pnf)

