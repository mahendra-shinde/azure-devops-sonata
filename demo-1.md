## ASP.NET WebAPI Project with Unit Test case

### Phases:
### 1. Create ASP.NET Web API project and Unit Test project
### 2. Create Project on Azure DevOps 
### 3. Push the Local project from visual studio to azure devops project
### 4. Create a Build pipeline and trigger a build
### 5. Create Release pipeline and release to azure app service.

## The Complete flow

## 1. Create new ASP.NET Web API using VS2019/VS2017

    1.1 New WebAPI with DOTNET CORE 2.1 and Docker Support
	Used "Linux" target 
	(DO NOT SELECT "Use same folder for solution and project)

    1.2 Once project is created, from "debug" toolbox 
	Select "MyAPI1" instead of "Docker"

    1.3 Open `ValuesController.cs` and modify the return type of method `Get` to `string`

```c#
[HttpGet("{id}")]
public String Get(int id)
{
    return "value";
}
```

    1.4 Run the project

    1.5 Add new project of type "MSTest Test Project(DotNet Core) within same solution.(Project name should end with `Tests`)

    1.6 Add reference to "MyAPI1" inside Test project

    1.7 Write following code in "testMethod1"
	
```c#
ValuesController cont = new ValuesController();
string value = cont.Get(0);
Assert.AreEqual("value", value,"Value did not match!");
```

## 2. Create new project on Azure DevOps with GIT repo
   
    2.1 Create new Project "MyApp1" on azure devops

    2.2 Make sure Version control selected is : Git

3. Push code into Azure Git Repo
    
    3.1 Open visual studio project, goto File -> Add to Source control to add local git repository (use name "MyApp1")

    3.2  goto "Team Explorer"
	there should be an option to PUSH repository to
	"Azure DevOps project"

    3.3 Make sure you click Advance button and choose project name `MyApp1` and Push code

4. Create Build Pipeline and Trigger a build

    4.1 Goto Azure DevOps portal, use Pipeline -> Build and then click `Create Build` or `New` to create new build pipeline.

    4.2 Click 'Use Classic Editor` to create classic build pipeline instead of YAML pipeline.

    4.3 Select default choice and click `Continue` , Select template `ASP.NET Core`

    4.4 Verify project names in build and test steps

    4.5 Save and trigger build

5. Create Release Pipeline and "Release" (Deploy)
	on azure app service.

    5.1 In Azure DevOps Portal, Goto `Pipelines` and then click `Releases` 

    5.2 Click `New Pipeline` button And then select template `Azure AppService deployment` and click Apply

    5.3 You need following details:

    ```ini
    Azure-Subscription= Choose azure subscription and authorize access to devops
    App-Service-Name= Name of Azure AppService (Use drop down)
    ```

    5.4 Save the pipeline and use `Release` button to create the release

    5.5 Once release is done, use `Deploy` button to start the deployment.
    