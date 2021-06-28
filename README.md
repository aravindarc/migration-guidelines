# migration-guidelines

This repo contains high level guidelines to migrate on-prem applications to containers.
Eventhough every technology can run on containers, the changes required is very different. This document contains steps for the following tech:

1. Java Spring
2. Java Spring Boot
3. Java Servlet
4. PHP Laravel
5. PHP Codeigniter
6. ASP.NET Core

# Directory Structure

Each tech stack has it's own directory, within which you can find guideline document and related Dockerfile or helm-chart.

```
.
+-- java-spring
|   +-- guideline.md
|   +-- Dockerfile
|   +-- helm-chart/
|   |   +-- chart.yml
|   |   +-- values.yml
|   |   +-- ...
+-- php-laravel
|   +-- guideline.md
|   +-- Dockerfile
|   +-- helm-chart/
|   |   +-- chart.yml
|   |   +-- values.yml
|   |   +-- ...
```
