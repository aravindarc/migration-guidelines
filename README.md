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

# How to find out what tech stack is your applicaition

`if`
* If your application has .java files, it will belong to **java spring or java spring boot or java servlet**.

    `if`

    * Do a global search `(ctrl + shift + f)` in the application for `@SpringBootApplication`, if you find that it is a **spring boot application**.

    `else if`

    * Do a search `(ctrl + f)` in the `pom.xml` for `spring`, if you find any occurrence, then it is **spring applicaiton**.

    `else`
    * It is a **java servlet** application.

`else if`

* If your application has .php files, it will belong to **php laravel or php codeigniter**.
    
    `if`
    
    * Find if there is a file called `artisan` in the root directory or if there is a `.env` file, if you find any of these it is **php laravel**.
    
    `else if`

    * Do a file search `(<ctrl + shift + n>PhpStorm, <ctrl+p>VsCode)` for a file called `CodeIgniter.php`, if you find this, it is **php codeigniter** application.

    `else`

    * It can be totally different frame like symfony or cakephp, documentation is missing for these, kindly raise a PR if you want to contribute.

`else if`

* If your application has .cs files, it will belong to **.net framework or .net core or asp.net framework or asp.net core**.

    `if`

    * Do a file search `(<ctrl + shift + n>PhpStorm, <ctrl+p>VsCode)` for a file called `.csproj`, if there is any occurrence it is a **.net core or asp.net core** application.

        `if`

        * Do a directory search `(<ctrl + shift + n>PhpStorm, <ctrl+p>VsCode)` for a file called `wwwroot`, if there is any occurrence it is **asp.net core** application.

        `else`

        * It is a **.net core** application.

    `else`

    * It is a **.net framework** application, which cannot be containerized and run on linux machines.
