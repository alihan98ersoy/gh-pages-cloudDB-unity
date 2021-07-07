---
title: Connect your game Huawei Mobile Services in 5 easy steps
description: 15
---

## Connect your game with Huawei Mobile Services in 5 easy steps

1. Register your app at Huawei Developer
2. Import the Plugin to your Unity project
3. Connect your game with the HMS Kit Managers



### 1 - Register your app at Huawei Developer

#### 

#### 1.1-  Register at [Huawei Developer](https://developer.huawei.com/consumer/en/)

#### 

#### 1.2 - Create an app in AppGallery Connect.

During this step, you will create an app in AppGallery Connect (AGC)  of HUAWEI Developer. When creating the app, you will need to enter the  app name, app category, default language, and signing certificate  fingerprint. After the app has been created, you will be able to obtain  the basic configurations for the app, for example, the app ID and the  CPID.

1. Sign in to Huawei Developer and click **Console**.
2. Click the HUAWEI AppGallery card and access AppGallery Connect.
3. On the **AppGallery Connect** page, click **My apps**.
4. On the displayed **My apps** page, click **New**.
5. Enter the App name, select App category (Game), and select Default language as needed.
6. Upon successful app creation, the App information page will  automatically display. There you can find the App ID and CPID that are  assigned by the system to your app.

#### 

#### 1.3 Add Package Name

Set the package name of the created application on the AGC.

1. Open the previously created application in AGC application management and select the **Develop TAB** to pop up an entry to manually enter the package name and select **manually enter the package name**.
2. Fill in the application package name in the input box and click save.

> Your package name should end in .huawei in order to release in App Gallery

#### 

#### Generate a keystore.

Create a keystore using Unity or Android Tools. make sure your Unity project uses this keystore under the **Build Settings>PlayerSettings>Publishing settings**

#### 

#### Generate a signing certificate fingerprint.

During this step, you will need to export the SHA-256 fingerprint by using keytool provided by the JDK and signature file.

1. Open the command window or terminal and access the bin directory where the JDK is installed.

2. Run the keytool command in the bin directory to view the signature file and run the command.

   `keytool -list -v -keystore D:\Android\WorkSpcae\HmsDemo\app\HmsDemo.jks`

3. Enter the password of the signature file keystore in the information  area. The password is the password used to generate the signature file.

4. Obtain the SHA-256 fingerprint from the result. Save for next step.

#### 

#### Add fingerprint certificate to AppGallery Connect

During this step, you will configure the generated SHA-256 fingerprint in AppGallery Connect.

1. In AppGallery Connect, click the app that you have created and go to **Develop> Overview**
2. Go to the App information section and enter the SHA-256 fingerprint that you generated earlier.
3. Click √ to save the fingerprint.

------

### 

### 2 - Import the plugin to your Unity Project

To import the plugin:

1. Download the [.unitypackage](https://github.com/EvilMindDevs/hms-unity-plugin/releases)
2. Open your game in Unity
3. Choose Assets> Import Package> Custom [![Import Package](https://camo.githubusercontent.com/fcdadb965895b9c98c9477fb5802433fb49d335ef58152f8a936807fd6aaa466/687474703a2f2f6576696c2d6d696e642e636f6d2f6875617765692f696d616765732f696d706f7274437573746f6d5061636b6167652e706e67)](https://camo.githubusercontent.com/fcdadb965895b9c98c9477fb5802433fb49d335ef58152f8a936807fd6aaa466/687474703a2f2f6576696c2d6d696e642e636f6d2f6875617765692f696d616765732f696d706f7274437573746f6d5061636b6167652e706e67)
4. In the file explorer select the downloaded HMS Unity plugin. The  Import Unity Package dialog box will appear, with all the items in the  package pre-checked, ready to install. [![image](https://user-images.githubusercontent.com/6827857/113576269-e8e2ca00-9627-11eb-9948-e905be1078a4.png)](https://user-images.githubusercontent.com/6827857/113576269-e8e2ca00-9627-11eb-9948-e905be1078a4.png)
5. Select Import and Unity will deploy the Unity plugin into your Assets Folder

------

### 

### 3 - Update your agconnect-services.json file.

In order for the plugin to work, some kits are in need of  agconnect-json file. Please download your latest config file from AGC  and import into Assets/StreamingAssets folder. [![image](https://user-images.githubusercontent.com/6827857/113585485-f488bd80-9634-11eb-8b1e-6d0b5e06ecf0.png)](https://user-images.githubusercontent.com/6827857/113585485-f488bd80-9634-11eb-8b1e-6d0b5e06ecf0.png)

------

### 

### 4 - Connect your game with any HMS Kit

In order for the plugin to work, you need to select the needed kits Huawei > Kit Settings. [![image](https://user-images.githubusercontent.com/6827857/113670088-57259c00-96bd-11eb-86d2-d53e4567fba1.png)](https://user-images.githubusercontent.com/6827857/113670088-57259c00-96bd-11eb-86d2-d53e4567fba1.png)

It will automaticly create the GameObject for you and it has  DontDestroyOnLoad implemented so you don't need to worry about reference being lost.