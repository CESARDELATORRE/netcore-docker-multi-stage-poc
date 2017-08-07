# aspnetapp MVC app with additional local reference to a .NET Core Class Library (MyDomainLayerLib) through a NuGet package and local NuGet source

The aspnetapp sample demonstrates how to Dockerize an ASP.NET Core app. If you'd like to see how to Dockerize a .NET Framework app check out the [.NET Framework Docker samples](https://github.com/Microsoft/dotnet-framework-docker-samples).

The instructions assume that you already have [.NET Core 1.1](https://www.microsoft.com/net/download/core#/sdk), [Git](https://git-scm.com/downloads), and [Docker](https://www.docker.com/products/docker) clients installed. They also assume you already know how to target Linux or Windows containers. Do try both image types. You need the latest Windows 10 or Windows Server 2016 to use [Windows containers](http://aka.ms/windowscontainers). For additional tutorials on ASP.NET Core see [ASP.NET Core Getting Started](https://www.asp.net/get-started).

Instructions
------------

Follow these steps to test and run the sample locally:
```console
cd aspnetapp
dotnet restore
dotnet run
```

Generate the NuGet package for the Library (Dependency on MyDomainLayerLib)
```console
cd MyDomainLayerLib
dotnet pack
```
Move the from MyDomainLayerLib.1.0.0.nupkg package file from the MyDomainLayerLib\bin\Debug to the local NuGet source: \aspnetapp\NugetPkgsLocalSource


Follow these steps to run this sample in a Linux or Windows container:

```console
docker build -t aspnetapp .
docker run -d -p 80:80 aspnetapp
```

```console
USING SPECIFIC TEST dockerfile.multi

docker build -t aspnetapp --file Dockerfile.multi .
docker run -d -p 5100:80 aspnetapp
```

## View your web page running from your container
* If you are using a linux container you can simply browse to http://localhost:80 to access your app in a web browser.
* If you are using the Nano [Windows Container](https://docs.docker.com/docker-for-windows/) there is currently a bug that affects how [Windows 10 talks to Containers via "NAT"](https://github.com/Microsoft/Virtualization-Documentation/issues/181#issuecomment-252671828) (Network Address Translation). Today you must hit the IP of the container directly. You can get the IP address of your container with the following steps:
  1. Run `docker ps` and copy the hash of your container ID
  3. Run `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" HASH` where `HASH` is replaced with your container ID.
  4. Copy the container ip address and paste into your browser with port 80. (Ex: 172.16.240.197:80)