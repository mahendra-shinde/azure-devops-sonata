Docker Commands:

Pull an image from registry (docker hub)
$ docker pull <IMAGENAME>

Pull an image from external / third party registry 
$ docker pull <RegistryURL>/<imagename>

Create and Launch a container in INTERACTIVE mode
$ docker run -it --name app1 <IMAGENAME> <PROCESS-NAME>
eg,
$ docker run -it --name app1 microsoft/nanoserver cmd

Create and launch a container in DEAMON mode
$ docker run -d --name app2 <IMAGENAME> <PROCESS-NAME>
eg:
$ docker run -d --name app1 microsoft/nanoserver ping -t 172.0.0.1
NOTE: The about command would keep the container ALIVE
