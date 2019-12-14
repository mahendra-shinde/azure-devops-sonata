## Build and release BASIC STATIC website

1.  Create new AzureDevOps project (static-site1)
2.  Goto Azure Repos and Use last option `Create Readme file`
3.  You should now get a Git repository with `Readme.md` file
4.  Click on `New` button and then choose `file`, 
    enter filename `index.htm` 
5.  Add following text to your file

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Home Page</title>
    </head>
    <body>
    <h2>Hello Bengaluru !</h2>
    </body>
    </html>
    ```
6.  Use `Commit` button to save the changes to repository.
7.  Create another file `Dockerfile` (Case sensitive) with these contents:

    ```ini
    ## Pull a base image which is lightweight and sufficient for this application
    FROM nginx:alpine

    ## COPY all HTML files into NGINX deployment folder
    ## Please refer to docker hub to know deployment folder
    ## https://hub.docker.com/_/nginx
    COPY *.htm    /usr/share/nginx/html/
    ```

8.  Goto `Project Settings` > Service Connections > choose `Docker Registry`

9.  Provide your docker-id and password, enter name for service connection `reg1` and click `Save and Verify`

9.  Goto `Azure Pipelines` and choose `New Pipeline`
    Use `Classic Editor` and then choose `Azure Repos Git` click `Continue`

10.  Choose template `Docker Container` and `Apply`

11. Click on `Variables` TAb and define a new variable `imagename` with value `mahendrshinde/static-app1`
    NOTE: Please replace `mahendrshinde` with your docker-id
12. Goto `Build an Image` step and set followings:
    
    ```yml
    Container-Registry-type:    Container registry
    Docker-Registry-Service-Connection: reg1
    Image-Name: $(imagename):$(Build.BuildId)
    ```

13. Goto `Push an image` steps and set followings:

    ```yml
    Container-Registry-type:    Container registry
    Docker-Registry-Service-Connection: reg1
    Image-Name: $(imagename):$(Build.BuildId)
    ```
14. Use `Save & Queue`

15. Create a new Azure App Service with deployment type "Docker Container" and OS Type "Linux"

16. The app service need container (Docker) setup, use "Single Container" with "Public" docker image `mahendrshinde/static-app1:23`
    NOTE: Please replace image name with your image.

17. Test the newly created azure app service in web browser, you should get message `Hello Bengalurur`

18. On Azure DevOps portal, use Release pipelines to create a new pipeline
    Use template `Azure App Service deployment`

19. Click on Build Artifacts and choose option "Docker Hub" provide following details:
    ```yml
    Service-connection: reg1 (Service Connection)
    Namespace:  mahendrshinde   (Docker ID)
    Repository: mahendrshinde/static-app1     (Projectname)
    Default-Version: Specify at the time of release
    ```

20. CLick on `Stage1` and provide details:
    ```yml
    Azure-Subscription : choose your azure subscription and authorize it
    App-Type:   WebApp for Containers (Linux)
    App-Service-Name: AppService created
    Registry-or-Namespace: mahendrshinde (Docker ID)
    Repository: static-app1 (Projectname)
    ```

21. Click on `Save` and then `Create Release` choose image version (TAG) from dropdown 
21. Once release is created, use `Deploy` button to start the deployment.