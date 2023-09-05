**Introduction**  
This document provides an overview of the NXphone Android SDK, including its functionality, parameters, and return value descriptions.

**SDK Usage**  
The NXphone-SDK project has been open-sourced to the Sonatype Central Repository. You can add the JAR package dependency to your configuration file as shown below.  
The Username and Password are the credentials used to call the NXphone-SDK, which can be generated and managed on the NXCloud platform.

Project Configuration  
- Main project Gradle configuration  
```
maven { url 'https://repo1.maven.org/maven2/' }
```
- App project Gradle configuration  
```
implementation 'com.nxcloud.nxphone:sips:0.0.21'
```
- Enable dataBinding in the module  
```
android {
    ...
    dataBinding {
        enabled = true
    }
    ...
}
```

**Soft Function Usage (NxcallSdkUtil)**

1) Get an instance of NxcallUtil. `NxcallSdkUtil.getInstance(Context context)`

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|context    |Yes  |Context |   Reference to the activity context. <br/>**Note: Do not mistakenly use the application context; use the context of the current activity instead!**   |  

2) Set the Nxcall phone listener (optional). `NxcallSdkUtil.setNxcallListener(NxcallListener nxcallListener)`

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|nxcallListener    |Yes  |NxcallListener |   None   |  

3) Initialize (must be initialized only once). `NxcallSdkUtil.init(Activity activity, View view, Chronometer mChronometer)`

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|activity   |Yes  |Activity  |   None   |
|view |No  |View |   Floating window view, can be null   |
|mChronometer |No  |Chronometer|   Chronometer for displaying time in the floating window, can be null   |  

4) Log in to the account. `boolean nxLogin(String username, String password)`

Regular login, which is faster, but the selected NXPhone access point may not be the optimal one. If there are call issues, our network operations center (NOC) needs to intervene to adjust the call quality.

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|username |Yes  |String  |   Account  |
|password |Yes  |String |   Password   |  

5) Speed test login. `boolean nxPreLogin(String username, String password)`

**> Note: Choose either regular login or speed test login, do not use both together!**  
NXPhone has multiple access points worldwide. Speed test login takes several seconds to automatically detect the network connection quality of each access point. After logging in, the call quality will be optimized. Note that this login method takes more time.

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|username |Yes  |String  |   Account  |
|password |Yes  |String |   Password   |  

6) Dial a number. `int nxcall(String number, String orderid)`

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|number |Yes  |String  |   Number to dial. If empty, it will automatically navigate to the number input interface; if not empty, it will directly dial the number  |
|orderid |No  |String |   Order ID, custom-defined by the customer to identify the queue. If empty, it will be automatically generated   |  

Return value `NxcallStateCode` corresponds to the dialing status.

|Return Value|Description|
|:----- |-----|
|1 |Success  |
|-1000 |Not logged in |
|-1001 |SIP not connected  |
|-1002 |Call in progress  |
|-1003 |Abnormal dialing number   |  

7) Destroy. `void onDestroy()`

|Parameter|Required|Type|Description|
|:----     |:---|:----- |-----              |
|None |  |  |     |  

- Example code steps

1) Initialization
```
NxcallSdkUtil.getInstance(getApplicationContext())
            .setNxcallListener(this) 
.init(this, null, null);
```
2) Login
```
NxcallSdkUtil.getInstance(getApplicationContext())
            .nxLogin("username", "password");
```
3) Dial a number
```
NxcallSdkUtil.getInstance(getApplicationContext())
            .nxcall("number", "orderid");
```
4) Destroy
```
NxcallSdkUtil.getInstance(getApplicationContext())
            .onDestroy();
```

**Troubleshooting**
1. Ensure that you are using NxcallSdkUtil.getInstance(mContext).nxLogin() correctly.
2. Check if there are multiple versions of the nxcall SDK dependencies in your project.
3. Perform a global search for nxPreLogin and nxLogin to see if there are multiple occurrences.