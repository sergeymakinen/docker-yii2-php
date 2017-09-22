# Yii 2 PHP Dockerfiles

This repository contains **Dockerfiles** of PHP CLI for Yii 2 tests on Ubuntu 16.04.02 LTS for [Docker](https://www.docker.com/)'s [automated build](https://hub.docker.com/r/sergeymakinen/yii2-php/) published to [Docker Hub](https://hub.docker.com/).

[![Build Type](https://img.shields.io/docker/automated/sergeymakinen/yii2-php.svg?style=flat-square)](https://hub.docker.com/r/sergeymakinen/yii2-php/) [![Total Stars](https://img.shields.io/docker/stars/sergeymakinen/yii2-php.svg?style=flat-square)](https://hub.docker.com/r/sergeymakinen/yii2-php/) [![Total Pulls](https://img.shields.io/docker/pulls/sergeymakinen/yii2-php.svg?style=flat-square)](https://hub.docker.com/r/sergeymakinen/yii2-php/) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)

## Supported tags and respective `Dockerfile` links

* `7.1` [(7.1/Dockerfile)](https://github.com/sergeymakinen/docker-yii2-php/blob/master/7.1/Dockerfile)
* `7.0` [(7.0/Dockerfile)](https://github.com/sergeymakinen/docker-yii2-php/blob/master/7.0/Dockerfile)
* `5.6` [(5.6/Dockerfile)](https://github.com/sergeymakinen/docker-yii2-php/blob/master/5.6/Dockerfile)

## What is Yii?

Yii is a free, open-source Web application development framework written in PHP5 that promotes clean, DRY design and encourages rapid development. It works to streamline your application development and helps to ensure an extremely efficient, extensible, and maintainable end product.

## Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://hub.docker.com/r/sergeymakinen/yii2-php/) from [Docker Hub](https://hub.docker.com/): 

```bash
docker pull sergeymakinen/yii2-php:tag
```

## How to use this image

#### Run tests

```bash
docker run -v ../Projects/yii2:/yii --rm sergeymakinen/yii2-php:tag vendor/bin/phpunit --group=sqlite --colors=always --verbose
```
