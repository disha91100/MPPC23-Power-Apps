# 🚀 Lab 5: Connect your own WebAPI to your Power App

> **Note:** This lab is optional. Only do this one when you are finished with lab 1 - lab 4.


### Estimated Duration: 75 minutes

## Lab Scenario

You are a developer at Contoso Ltd exploring ways to extend the capabilities of Power Apps by integrating external services. Your team wants to connect custom backend APIs to Power Platform solutions to expose complex business logic and data that cannot be handled directly within Dataverse. In this optional lab, you will build a simple ASP.NET Core Web API using Visual Studio, register it as a custom connector through a dev tunnel, and consume it in a canvas app. This scenario mimics real-world enterprise integration patterns where external APIs are connected securely to low-code applications.

## Lab Objectives

In this lab, you will go though the following tasks:

- Task 1: Create an ASP.NET project in Visual Studio
- Task 2: Add Power Platform as a connected service
- Task 3: Create a canvas app with the custom connector

## Task 1: Create an ASP.NET project in Visual Studio

In this task, we will create an ASP.NET project in Visual Studio.

1. Search for **Visual Studio 2022 (1)** and then select **Visual Studio 2022 (2)**.

    ![TODO](./assets/bs132.png)

1. Select **Create a new project**.

    ![TODO](./assets/bs133.png)

1. If no tools are installed, click **Install more tools and features**. This opens the Visual Studio Installer.

    ![TODO](./assets/bs133_1.png)

2. Verify that the **ASP.NET and web development (1)** workload is installed. If not, select it and click **Modify (2)** to install.

     ![TODO](./assets/bs133_2.png)

1. If a pop-up appears asking to save your work, select **Continue**. After the installation finishes, restart Visual Studio 2022 and choose **Create a new project**.

     ![TODO](./assets/bs133_3.png)

1. Search for `ASP.NET Core Web API` **(1)**, select `ASP.NET Core Web API` **(2)** the one that has **C# (3)** in the tags and select **Next (4)**.

    ![TODO](./assets/bs134.png)

1. Enter the following details and select **Next (3)**:

   - Enter `WeatherSample` for the Project name **(1)**

   - Enter `C:\Dev` for the Location **(2)**

     ![TODO](./assets/bs135.png)   

1. In the next screen, select **Create**.

    ![TODO](./assets/bs136.png)

1. This should create your ASP.NET Code Web API project and open it in Visual Studio 2022.

    ![TODO](./assets/bs137.png)

1. Navigate to **Tools (1)** from the top menu and then select **Options (2)**.

    ![TODO](./assets/bs138.png)

1. Scroll down, then expand **Nuget Package Manager (1)** then select **Package Sources (2)** and make sure `nuget.org` package is added **(3)**. If present click on **Cancel (4)**.

    ![TODO](./assets/bs139.png)

    >**Note**: Please follow the below steps if `nuget.org` package is not added

    - Click on the **+** symbol to add the package

      ![TODO](./assets/bs140.png)

    - Provide the **Name** as `nuget.org` **(1)** then **Source** as `https://api.nuget.org/v3/index.json` **(2)** then click on **Update (3)** and then **OK (4)**

      ![TODO](./assets/bs141.png)    

1. From the **Solution Explorer**, right click on the **WeatherSample** project.

    ![TODO](./assets/bs142.png)

1. Select **Manage NuGet Packages**.

    ![TODO](./assets/bs143.png)

1. Select **Installed (1)** tab, then make sure that `Swashbuckle.AspNetCore` is installed **(2)**.

    ![TODO](./assets/bs144.png)
   
   - If not, navigate to **Browse** tab

     ![TODO](./assets/bs145.png)  

   - Search for `Swashbuckle.AspNetCore`, then click on **Install**    

   - Make sure `Swashbuckle.AspNetCore` is installed

## Task 2: Add Power Platform as a connected service

In this task, you will add the Connected Service for Power Platform to your ASP.NET Code Web API project.

1. In **Solution Explorer**, right-click the **Connected Services** node.

    ![TODO](./assets/bs146.png)

1. Select **Manage Connected Services** from the context menu.

    ![TODO](./assets/bs147.png)

1. In the **Connected Services** tab, select the **+** icon for **Service Dependencies**.

    ![TODO](./assets/bs148.png)

1. On the **Add dependency** dialog, type `Power Platform` into the search box then select **Microsoft Power Platform (2)** and then **Next (3)**.

    ![TODO](./assets/bs149.png)

     >**Note**: If you aren't signed in already, sign into your Microsoft Power Platform account. If you don't have a Power Platform account, [Create a Developer Environment](create-developer-environment.md).

1. In the **Connect to Microsoft Power Platform** screen

   - Select your developer environment
   - **Power Platform Solution**: Select **MPPC 23 (1)**
   - In **Custom connectors name**, the value `WeatherSample_Connector` should already be set **(2)**

        > **Note:** If you don't see your connectors, click the **+** icon next to **Custom connectors name**. Create a new connector from blank, select the **dev** environment, name it `WeatherSample_Connector`, and then select **Create**.

   - In **Select a public dev tunnel**, select the **+ (3)** icon

     ![TODO](./assets/bs150.png) 

1. Click **Next**. 

1. On the **Account** page, provide the following details:      

   - In the field **Name**, type `SampleTunnel` **(1)**

   - Select **Tunnel Type**: **Persistent** **(2)**

   - Select **Access** : **public** **(3)**

   - Select **OK** **(4)**

     ![TODO](./assets/bs151.png)    

1. Select **Finish**.

    ![TODO](./assets/bs152.png)

1. Once the connected service is configured, select **Close**.

    ![TODO](./assets/bs153.png)

1. Click on **Build (1)** and then **Build Solution (2)**.
 
    ![TODO](./assets/bs154.png)

## Task 3: Create a canvas app with the custom connectorI

This task guides you through creating a canvas app that connects to your ASP.NET Web API via a custom connector and displays data in a gallery.

> **Note:** When running a web app in Visual Studio with a tunnel active, the browser will open to a tunnel URL instead of `localhost`.

1. **Run the API**
   - Open your Visual Studio solution and start debugging.
   - When the browser opens to the tunnel URL, a warning page will appear.  
     Select **Continue**.

2. **Open Power Apps**, In a new browser tab, go to [Power Apps](https://make.powerapps.com). Select your **Dev** environment from the upper-right corner.

3. Select **+ Create (1)** and the **Start with blank canvas (2)**.  

     ![Create Blank App](./assets/L5T3_2.png)

   - Then choose the **Phone** format. Skip the tutorial if prompted.

     ![Canvas App from Blank](./assets/L5T3_1.png)

4. **Add a Data Connection**
   - From the top menu, select **Add data**.

     ![Add Data](./assets/L5T3_3.png)

   - Search for and select **WeatherSample_Connector**, then choose **Connect**.  
     For more details, see [Add connections to your canvas app](https://learn.microsoft.com/power-apps/maker/canvas-apps/add-data-connection).

5. **Insert a Button**
   - Insert a **Button** control and move it to the bottom of the screen.

     ![Insert Button](./assets/L5T3_4.png)

   - With the button selected, set the **Text** property to `Load Data`.  

     ![Set Button Text](./assets/L5T3_5.png)

6. **Configure Button Action**
   - Set the button’s **OnSelect** property to the following formula:
     ```powerapps-dot
     ClearCollect(weatherCollection, WeatherSample_Connector.GetWeatherForecast())
     ```
     ![Set Button Formula](./assets/L5T3_6.png)

1. **Insert a Gallery**
   - Go to the **Insert** tab, search for **Blank Vertical Gallery**, and select it. 

     ![Insert Gallery](./assets/L5T3_8.png)

2. **Connect the Gallery to Data**
   - Set the gallery’s **Data source** to **weatherCollection**.
   - Change the **Layout** to **Title and subtitle**. 

     ![Set Gallery Data Source](./assets/L5T3_8.png)

1. **Run the App**  
   - Select the **Play** icon in the top-right corner of the screen to run the app.  
   - The app should display similar to the example below:
    
        ![Screenshot of a Power Apps canvas app created using the sample ASP.NET Weather web API.](./assets/vs-powerapp.png)

## Review

In this lab you have completed the following tasks:

- Created an ASP.NET project in Visual Studio
- Added Power Platform as a connected service
- Created a canvas app with the custom connector


### Congratulations! you have successfully completed this lab.

