Power Apps Hands on
---

# 1. Environment prep and logins

## 1.1. Setting up Power Apps community plan

If you already have a community plan setup,<br>
you can skip this step.

1. Access the Power Apps community plan site<br>
https://powerapps.microsoft.com/en-us/communityplan/

2. Click on Get Started Free
![](pasteimage/2020-03-15-19-36-01.png)

3. Sign-up
![](pasteimage/2020-03-15-19-38-11.png)
Note: you cannot use personal mails like Gmail or Hotmail.

4. Authenticate with phone or SMS if requested <br>

5. If requested, enter the acquired authorization code to authenticate
![](pasteimage/2020-03-15-19-44-13.png)

6. Enter your account details and click Start
![](pasteimage/2020-03-15-19-47-05.png)

## 1.2. Register for Azure

If you already have an Azure environment, you can skip this step.

1. Access Azure website<br>
https://azure.microsoft.com/ja-jp/


2. Click on Start Free 
![](pasteimage/2020-03-17-05-50-31.png)

3. Click on Start free again<br>
![](pasteimage/2020-03-17-05-51-25.png)

4. Login with your Microsoft Account or GitHub account<br>
![](pasteimage/2020-03-17-05-54-27.png)

5. Fill-in the necessary details and click on Sign up
![](pasteimage/2020-03-17-06-11-48.png)


# 2. Preparing Azure

## 2.1. Create a resource group

1. Click on Resource Groups<br>
![](pasteimage/2020-03-16-03-45-02.png)

2. Click Add<br>
![](pasteimage/2020-03-16-03-45-57.png)

3. Set the parameters for resource group as below<br>
![](pasteimage/2020-03-16-03-50-08.png)

4. Click Create<br>
![](pasteimage/2020-03-16-03-51-44.png)

## 2.2. Creating Storage Account

1. Go to the resouce group you created, and click Add<br>
![](pasteimage/2020-03-16-03-55-20.png)

2. Select Storage Account<br>
![](pasteimage/2020-03-16-04-01-02.png)

3. Setup the details like below<br>
![](pasteimage/2020-03-16-04-05-47.png)

4. Click Create<br>
![](pasteimage/2020-03-16-04-07-01.png)

5. Once deployment is complete, click on Go to Resource<br>
![](pasteimage/2020-03-16-04-07-02.png)

6. Click on Containers<br>
![](pasteimage/2020-03-16-04-07-03.png)

7. Click on +Container
![](pasteimage/2020-03-16-04-07-04.png)

8. Specify like below and click Create<br>
![](pasteimage/2020-03-16-04-07-05.png)

9. Go to Access Keys, and obtain the Key from key1<br>
![](pasteimage/2020-03-16-04-07-06.png)

## 2.3. Create a Face API

1. Go to the resouce group you created, and click Add<br>
![](pasteimage/2020-03-16-03-55-20.png)

2. Select Face<br>
![](pasteimage/2020-03-16-04-12-43.png)

3. Click Create<br>
![](pasteimage/2020-03-16-04-12-27.png)

4. Setup the details like below<br>
![](pasteimage/2020-03-16-04-15-34.png)

5. Click on Go to Resource<br>
![](pasteimage/2020-03-16-04-15-35.png)

6. Obtain the codes from Key1<br>
![](pasteimage/2020-03-16-04-15-36.png)

# 3. Create a facial recognition app with Power Apps

## 3.1. Open Power Apps

1. Open Power Apps from https://make.powerapps.com<br>
![](pasteimage/2020-03-16-23-39-29.png)

2. Click Create Canvas App from blank<br>
![](pasteimage/2020-03-16-23-56-19.png)

3. Select Tablet as the choice of app type<br>
![](pasteimage/2020-03-17-00-09-18.png)

4. Power Apps studio will show up<br>
![](pasteimage/2020-03-17-00-17-51.png)

## 3.2. Make screens

### 3.2.1. Person Group 作成画面
In order to setup facial recognition using Face API you need to first setup a "Person Group" to register the user. We will first create a screen for that.

1. Change the screen name<br>
![](pasteimage/2020-03-17-00-40-43.png)
![](pasteimage/2020-03-17-00-41-34.png)

2. Open Datasources<br>
![](pasteimage/2020-03-17-00-56-15.png)

3. Select Face API<br>
![](pasteimage/2020-03-17-01-08-27.png)

4. Paste the Face API key. You will only need to do this for the first time.<br>
![](pasteimage/2020-03-17-01-10-01.png)

5. Go back to tree view<br>
![](pasteimage/2020-03-17-01-14-44.png)
![](pasteimage/2020-03-17-01-14-56.png)

6. Create a Textbox to enter the Person Group ID<br>
![](pasteimage/2020-03-17-01-15-47.png)
![](pasteimage/2020-03-17-01-16-09.png)

7. Change the name of Textbox to "PersonGroupIDInput"<br>
![](pasteimage/2020-03-17-01-17-08.png)
![](pasteimage/2020-03-17-01-47-38.png)

8. Change the property of PersonGroupIDInput to the following.<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Default|Default||
|HintText|Hint Text|Set the Person ID here|

![](pasteimage/2020-03-17-01-33-28.png)

9. Create a lable for PersonIDInput<br>
![](pasteimage/2020-03-17-01-43-25.png)

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|Person Group ID|

![](pasteimage/2020-03-17-01-44-59.png)

10. Also create the Textbox for Person Group Name as PersonGroupNameInput<br>
![](pasteimage/2020-03-17-01-48-25.png)

11. Create a button PersonGroupSubmitButton<br>
![](pasteimage/2020-03-17-01-50-28.png)

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|Register|

![](pasteimage/2020-03-17-02-18-21.png)

12. PersonGroupSubmitButton の OnSelect プロパティに以下を指定する。

``` php
//Person Group 作成処理
FaceAPI.CreatePersonGroup(PersonGroupIDInput.Text,PersonGroupNameInput.Text);
```

13. Change the DisplayMode property of PersonGroupSubmitButton to below:

``` php
//If ID and Name is not populated, disable button.
If(Or(IsBlank(PersonGroupIDInput.Text),IsBlank(PersonGroupNameInput.Text)),DisplayMode.Disabled,DisplayMode.Edit)

//Move to PersonAddScreen
Navigate(PersonAddScreen,ScreenTransition.Fade)

```

### 3.2.2. Screen for Person

1. Add a new blank screen and name it PersonAddScreen<br>
![](pasteimage/2020-03-17-02-30-05.png)

2. Open Ddatasources<br>

3. Select Azure Blob Storage<br>
![](pasteimage/2020-03-17-03-30-25.png)

4. Paste the Azure Blob Storage API key. You will only need to do this for the first time.<br>
![](pasteimage/2020-03-17-03-32-07.png)

5. Add a camera control and change the name to PersonAddCam<br>
![](pasteimage/2020-03-17-03-34-33.png)
![](pasteimage/2020-03-17-04-29-05.png)

6. Add a dropdown box name this PersonAddCamSelect<br>
![](pasteimage/2020-03-17-03-36-34.png)

|Property Name|Display Name|Value|
|:--|:--|:--|
|Items|--|[0,1,2]|
|Default|Default|0|

7. Change the properties of PersonAddCam to below<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Camera|Camera|PersonAddCamSelect.SelectedText.Value|
|StreamRate|Stream Rate|100|

8. Create a Textbox and a label to enter the Person Name. Name this as PersonNameInput and PersonNameLabel respectively<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Default|Default||
|HintText|Hint Text|Set Person Name here|

9. 登録用のボタン(PersonSubmitButton)を作成する。<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|テキスト|登録|

![](pasteimage/2020-03-17-04-27-46.png)

10. PersonSubmitButton の OnSelect プロパティに以下を指定する。

``` php
//Create Person data
Set(PersonID,FaceAPI.CreatePerson(PersonGroupIDInput.Text,PersonNameInput.Text));

//Upload image for face registeration
AzureBlobStorage.CreateBlockBlob("<Container Name>","learn.jpg",PersonAddCam.Stream);

//General URL to register for face registeration
Set(learnimageuri,AzureBlobStorage.CreateShareLinkByPath("<Container Name>/learn.jpg"));

//Register face
FaceAPI.AddPersonFace(PersonGroupIDInput.Text,PersonID.personId,learnimageuri.WebUrl);

//Move to FaceAuthenticationScreen
Navigate(FaceAuthenticationScreen,ScreenTransition.Fade)
```

11. Change the DisplayMode property to the following for PersonSubmitButton

``` php
//If name is not entered, disable button
If(IsBlank(PersonNameInput.Text),DisplayMode.Disabled,DisplayMode.Edit)
```

### 3.2.3. Create facial recognition screen

1. Add a new blank screen and set the name to FaceAuthenticationScreen<br>

2. Add a dropdown box and name it AuthenticateCamSelect<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Items|--|[0,1,2]|
|Default|Default|0|

3. Add a camera control, and name it AuthenticateCam<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Camera|Camera|AuthenticateCamSelect|
|StreamRate|Streaming rate|100|

4. Create a button to start facial recognition. Name it AuthenticateSubmitButton<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|Recognize Face|

5. AuthenticateSubmitButton の OnSelect プロパティに以下を指定する。

``` php
//Upload image for facial recognition
AzureBlobStorage.CreateBlockBlob("<Container Name>","authenticate.jpg",AuthenticateCam.Stream);

//Generate URL for facial recognition image
Set(autenticateimageuri,AzureBlobStorage.CreateShareLinkByPath("<Container Name>/authenticate.jpg"));

//Retrieve image
Set(FaceIDdata,FaceAPI.Detect(autenticateimageuri.WebUrl,{returnFaceId:"true"}));

//Obtain recognition results
Set(FaceVerify,FaceAPI.Verify(First(FaceIDdata).faceId,PersonGroupIDInput.Text,PersonID.personId))

//Store result to a temporary table
Collect(AuthenticateLog,{
    DateTime:Now(),
    AuthResult:If(FaceVerify.isIdentical,"Face Verified","Unknown Face"),
    MatchLate:FaceVerify.confidence
    }
)
```

6. Create a label to display recognition results. Name it AuthenticateResultLabel<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|テキスト|If(FaceVerify.isIdentical,"Face Verified","Unknown Face")|
|Align|テキストのアラインメント|Align.Right|

7. Create a label to display confidence percentage. Name this MatchRateLabel<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|Concatenate("Confidence: ",Text(Round((FaceVerify.confidence*100),2)),"%")|
|Align|Text alignment|Align.Right|

![](pasteimage/2020-03-17-05-09-50.png)

### 3.2.4. Create a results screen

1. Add a new blank screen and name it ResultScreen<br>

2. Add a Gallery and name it ResultGallary<br>
![](pasteimage/2020-03-17-07-01-59.png)

3. Select AuthenticateLog as datasource<br>
![](pasteimage/2020-03-17-07-03-30.png)

4. Change layout to "Title, subtitle, body"<br>
![](pasteimage/2020-03-17-07-04-54.png)

5. Click Edit on the field and change settings to below.
![](pasteimage/2020-03-17-07-07-04.png)

|Field Name|Value|
|:--|:--|
|Body1|MatchRate|
|Subtitle1|AuthResult|
|Title1|DateTime|

6. Click on Body1 in the tree view, and change the Text property to below:<br>

``` php
Concatenate("Match :",Text(Round((ThisItem.MatchRate*100),2)),"%")
```

![](pasteimage/2020-03-17-07-11-54.png)


### 3.2.5. Create a home screen

1. Add a new blank screen and name it HomeScreen<br>

2. Add a label and name it TitleLabel<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|"Facial Recognition App"|
|Size|Font size|40|

3. Add a button and name it MovePersonAddSCButton to move to PersongroupAddScreen<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|"Registeration"|

4. Change the OnSelect property of MovePersonAddSCButton to below.

``` php
//Move to PersongroupAddScreen
Navigate(PersongroupAddScreen,ScreenTransition.Fade)
```

5. Create a button and name it MoveFaceAuthenticationSCButton to move to FaceAuthenticationScreen<br>

|Property Name|Display Name|Value|
|:--|:--|:--|
|Text|Text|"Recognition"|

6. Change the OnSelect property of MoveFaceAuthenticationSCButton to below.

``` php
//Move to PersongroupAddScreen
Navigate(FaceAuthenticationScreen,ScreenTransition.Fade)
```

7. Change the DisplayMode property of MoveFaceAuthenticationSCButton to below.

``` php
//If Name is not entered, disable the button.
If(IsBlank(PersonNameInput.Text),DisplayMode.Disabled,DisplayMode.Edit)
```
8. Add a button and name it MoveResultSCButton to move to ResultScreen<br>

|Property|Display Name|Value|
|:--|:--|:--|
|Text|Text|"History Screen"|

9. Change the OnSelect property of MoveResultSCButton to below.

``` php
//Move to PersongroupAddScreen
Navigate(ResultScreen,ScreenTransition.Fade)
```

### 3.2.6. Add the Back navigation button

1. Go to PersongroupAddScreen<br>

2. Select Back from list of icons<br>
![](pasteimage/2020-03-17-07-15-48.png)

3. Change the OnSelect property to below<br>
``` php
//Go to the previous screen
Back(ScreenTransition.Fade)
```
4. Copy and paste the icon to every screen except the HomeScreen<br>

### 3.2.7. Changing the order of HomeScreen

To make sure the app shows the HomeScreen first when the app is launched, change the order of HomeScreen to be at the top.

![](pasteimage/2020-03-17-07-23-43.png)

![](pasteimage/2020-03-17-07-24-14.png)


## 3.3. Testing the app

Press the play button on the top right corner of the screen to try your app out.

![](pasteimage/2020-03-17-05-13-25.png)

## 3.4. Saving the app

Go to File, select Save to save your current app configuration.

![](pasteimage/2020-03-17-05-14-40.png)
![](pasteimage/2020-03-17-05-16-04.png)

By clicking Publish, you can now run the app on your smartphone devices.

![](pasteimage/2020-03-17-05-17-11.png)

# 4. Try out the app on your device

Try running the app on your device to see if it works!