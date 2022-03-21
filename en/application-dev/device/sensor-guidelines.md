# Sensor Development


## When to Use

- Data provided by the compass sensor denotes the current orientation of the user device, which helps your application accurately navigate for the user.

- Data provided by the proximity sensor denotes the distance between the device and a visible object, which enables the device to automatically turn on or off its screen accordingly to prevent accidental touch on the screen.

- Data provided by the barometer sensor helps your application accurately determine the altitude of the device.

- Data provided by the ambient light sensor helps your device automatically adjust its backlight.

- Data provided by the Hall effect sensor implements the smart cover mode of your device.

- Data provided by the heart rate sensor helps your application track the health of a user.

- Data provided by the pedometer sensor helps your application obtain the number steps a user has walked.

- Data provided by the wear detection sensor helps your application detect whether a user is wearing a wearable device.


## Available APIs

  | Module | API | Description | 
| -------- | -------- | -------- |
| ohos.sensor | sensor.on(sensorType,callback:AsyncCallback&lt;Response&gt;):void | Subscribes to data changes of a type of sensor. | 
| ohos.sensor | sensor.once(sensorType,callback:AsyncCallback&lt;Response&gt;):void | Subscribes to only one data change of a type of sensor. | 
| ohos.sensor | sensor.off(sensorType,callback:AsyncCallback&lt;void&gt;):void | Unsubscribes from sensor data changes. | 


## How to Develop

1. To obtain data from a type of sensor, configure the request permissions in the **config.json** file.
  
   ```
   "reqPermissions":[
     {
        "name":"ohos.permission.ACCELEROMETER",
        "reason"":"", 
        "usedScene":{
         "ability": ["sensor.index.MainAbility",".MainAbility"],
         "when":"inuse"
       }
     },
     {
        "name":"ohos.permission.GYROSCOPE",
        "reason"":"", 
        "usedScene":{
         "ability": ["sensor.index.MainAbility",".MainAbility"],
         "when":"inuse"
       }
     },
     {
        "name":"ohos.permission.ACTIVITY_MOTION",
        "reason"":"ACTIVITY_MOTION_TEST", 
        "usedScene":{
         "ability": ["sensor.index.MainAbility",".MainAbility"],
         "when":"inuse"
       }
     },
     {
        "name":"ohos.permission.READ_HEALTH_DATA",
        "reason"":"HEALTH_DATA_TEST", 
        "usedScene":{
         "ability": ["sensor.index.MainAbility",".MainAbility"],
         "when":"inuse"
       }
     },
     {
        "name":"ohos.permission.VIBRATE",
        "reason"":"", 
        "usedScene":{
         "ability": [".MainAbility"],
         "when":"inuse"
       }
     },
   ]
   ```

2. Subscribe to data changes of a type of sensor.
  
   ```
   import sensor from "@ohos.sensor"
   sensor.on(type:sensorType,function(error,data){
       if (error) {// The call fails, and error.code and error.message are printed.
           console.error("Subscription failed. Error code: " + error.code + "; message: " + error.message);
           return;
       };
          console.info("Subscription succeeded. data = "+ data);// The call is successful, and the obtained sensor data is printed.
     }
   );
   ```

   The following figure shows the successful call result when **SensorType** is **SENSOR_TYPE_ID_ACCELEROMETER**.

   ![en-us_image_0000001241693881](figures/en-us_image_0000001241693881.png)

3. Unsubscribe from sensor data changes.
  
   ```
   import sensor from "@ohos.sensor"
   sensor.off(type:sensorType,function(error) {
       if (error) {// The unsubscription fails, and error.code and error.message are printed.
           console.error("Failed to unsubscribe from acceleration sensor data. Error code: " + error.code + "; message: " + error.message);
           return;
       };
       console.info("Succeeded in unsubscribing from acceleration sensor data.");// The unsubscription is successful, and the result is printed.
     }
   );
   ```

   The following figure shows the successful call result when **SensorType** is **SENSOR_TYPE_ID_ACCELEROMETER**.

   ![en-us_image_0000001196654004](figures/en-us_image_0000001196654004.png)

4. Subscribe to only one data change of a type of sensor.
  
   ```
   import sensor from "@ohos.sensor"
   sensor.once(tyep:sensorType,function(error, data) {
       if (error) {// The call fails, and error.code and error.message are printed.
           console.error("Failed to obtain data. Error code: " + error.code + "; message: " + error.message);
           return;
       };
           console.info("Data obtained successfully. data="+data);// The call is successful, and the obtained sensor data is printed.
     }
   );
   ```

   The following figure shows the successful call result when **SensorType** is **SENSOR_TYPE_ID_ACCELEROMETER**.

   ![en-us_image_0000001241733907](figures/en-us_image_0000001241733907.png)
