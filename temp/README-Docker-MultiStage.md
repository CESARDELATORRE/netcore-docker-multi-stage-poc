Follow these steps to run the WebMVC in a Linux or Windows container:

```console
docker build -t webmvc-multi:last --file Dockerfile.multi .
docker run -d -p 5100:80 webmvc-multi
```

## View your web page running from your container
* If you are using a linux container you can simply browse to http://localhost:5100 to access your app in a web browser.
* If you are using the Nano [Windows Container](https://docs.docker.com/docker-for-windows/) there is currently a bug that affects how [Windows 10 talks to Containers via "NAT"](https://github.com/Microsoft/Virtualization-Documentation/issues/181#issuecomment-252671828) (Network Address Translation). 
Today you must hit the IP of the container directly. You can get the IP address of your container with the following steps:
  1. Run `docker ps` and copy the hash of your container ID
  3. Run `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" HASH` where `HASH` is replaced with your container ID.
  4. Copy the container ip address and paste into your browser with port 80. (Ex: 172.16.240.197:80)