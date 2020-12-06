<a name="BOTVAC"></a>

# BOTVAC

<ul>

This module controls Neato Botvac Connected and Vorwerk Robot Vacuums.  
For issuing commands or retrieving Readings it's necessary to fetch the information from the NEATO/VORWERK Server.
In this way, it can happen, that it's not possible to send commands to the Robot until the corresponding Values are fetched.
This means, it can need some time until your Robot will react on your command.  
  
**<a name="BOTVACdefine"></a>Define**

<ul>

`define <name> BOTVAC <email> [NEATO|VORWERK] [<polling-interval>]`  
  
Example:
`define myNeato BOTVAC myemail@myprovider.com NEATO 300`  
  
After defining the Device, it's necessary to enter the password with
`set <name> password <password>`  
It is exactly the same Password as you use on the Website or inside the App.

Example:
`set NEATO passwort mySecretPassword`  

</ul>

**<a name="BOTVACget"></a>Get**

* <a name="batteryPercent"></a>`get <name> batteryPercent`  
  requests the state of the battery from Robot
* <a name="statistics"></a>`get <name> statistics`  
  display statistical data, extracted from available maps of recent cleanings

**<a name="BOTVACset"></a>Set**

* <a name="findMe"></a>`set <name> findMe`  
  plays a sound and let the LED light for easier finding of a stuck robot
* <a name="dismissCurrentAlert"></a>`set <name> dismissCurrentAlert`  
  reset an actual Warning (e.g. dustbin full)
* <a name="nextCleaningMode"></a>`set <name> nextCleaningMode`  
  Depending on Model, there are Arguments available: eco/turbo
* <a name="nextCleaningModifier"></a>`set <name> nextCleaningModifier`  
  The modifier is used for next spot cleaning.
  Depending on Model, there are Arguments available: normal/double
* <a name="nextCleaningNavigationMode"></a>`set <name> nextCleaningNavigationMode`  
  The navigation mode is used for the next house cleaning.
  Depending on Model, there are Arguments available: normal/extraCare/deep
* <a name="nextCleaningZone"></a>`set <name> nextCleaningZone`  
  Depending on Model, the ID of the zone that will be used for the next zone cleaning can be set.
* <a name="nextCleaningSpotHeight"></a>`set <name> nextCleaningSpotHeight`  
  Is defined as number between 100 - 400. The unit is cm.
* <a name="nextCleaningSpotWidth"></a>`set <name> nextCleaningSpotWidth`  
  Is defined as number between 100 - 400. The unit is cm.
* <a name="password"></a>`set <name> password <password>`  
  set the password for the NEATO/VORWERK account
* <a name="pause"></a>`set <name> pause`  
  interrupts the cleaning
* <a name="pauseToBase"></a>`set <name> pauseToBase`  
  stops cleaning and returns to base
* <a name="reloadMaps"></a>`set <name> reloadMaps`  
  load last map from server into the cache of the module. no file is stored!
* <a name="resume"></a>`set <name> resume`  
  resume cleaning after pause
* <a name="schedule"></a>`set <name> schedule`
  on and off, switch time control
* <a name="sendToBase"></a>`set <name> sendToBase`  
  send roboter back to base
* <a name="setBoundariesOnFloorplan"></a>`set <name> setBoundariesOnFloorplan_<floor plan> <name|{JSON String}>`  
  Set boundaries/nogo lines in the corresponding floor plan.
  The paramter can either be a name, which is already defined by attribute "boundaries", or alternatively a JSON string. (A comma-separated list of names is also possible.)  
  [Description of syntax](https://developers.neatorobotics.com/api/robot-remote-protocol/maps)  
  Examples:  
  `set <name> setBoundariesOnFloorplan_0 Bad`  
  `set <name> setBoundariesOnFloorplan_0 Bad,Kueche`  
  `set <name> setBoundariesOnFloorplan_0 {"type":"polyline","vertices":[[0.710,0.6217],[0.710,0.6923]], "name":"Bad","color":"#E54B1C","enabled":true}`
* <a name="setRobot"></a>`set <name> setRobot`  
  choose robot if more than one is registered at the used account
* <a name="startCleaning"></a>`set <name> startCleaning ([house|map|zone])`  
  start the Cleaning from the scratch.
  If the robot supports boundaries/nogo lines/zones, the additional parameter can be used as:
  * `house` - cleaning without a persisted map
  * `map` - cleaning with a persisted map
  * `zone` - cleaning in a specific zone, set zone with nextCleaningZone
* <a name="startSpot"></a>`set <name> startSpot`  
  start spot-Cleaning from actual position.
* <a name="startManual"></a>`set <name> startManual`  
  start Manual Cleaning.
  This cleaning mode opens a direct websocket connection to the robot.
  Therefore robot and FHEM installation has to reside in the same LAN.
  Even though an internet connection is necessary as the initialization is triggered by a remote call.  
  *Note:* If the robot does not receive any messages for 30 seconds it will exit Manual Cleaning, but it will not close the websocket connection automaticaly.
* <a name="statusRequest"></a>`set <name> statusRequest`  
  pull update of all readings. necessary because NEATO/VORWERK does not send updates at their own.
* <a name="stop"></a>`set <name> stop`  
  stop cleaning and in case of manual cleaning mode close also the websocket connection
* <a name="syncRobots"></a>`set <name> syncRobots`  
  sync robot data with online account.
  Useful if one has more then one robot registered
* <a name="pollingMode"></a>`set <name> pollingMode <on|off>`  
  set polling on (default) or off like attribut disable.
* <a name="robotSounds"></a>`set <name> robotSounds <on|off>`  
  set sounds on or off.
* <a name="dirtbinAlertReminderInterval"></a>`set <name> dirtbinAlertReminderInterval <30|60|90|120|150>`  
  set alert intervall in minutes.
* <a name="filterChangeReminderInterval"></a>`set <name> filterChangeReminderInterval <1|2|3>`  
  set alert intervall in months.
* <a name="brushChangeReminderInterval"></a>`set <name> brushChangeReminderInterval <4|5|6|7|8>`  
  set alert intervall in months.
* <a name="wsCommand"></a>`set <name> wsCommand`  
  Commands start or stop cleaning activities.
  * `eco-on`
  * `eco-off`
  * `turbo-on`
  * `turbo-off`
  * `brush-on`
  * `brush-off`
  * `vacuum-on`
  * `vacuum-off`
* <a name="wsCombo"></a>`set <name> wsCombo`  
  Combos specify a behavior on the robot.  
  They need to be sent with less than 1Hz frequency.
  If the robot doesn't receive a combo with the specified frequency it will stop moving.
  Also, if the robot does not receive any messages for 30 seconds it will exit Manual Cleaning.
  * `forward` - issues a continuous forward motion.
  * `back` - issues a discontinuous backward motion in ~30cm intervals as a safety measure since the robot has no sensors at the back.
  * `arc-left` - issues a 450 turn counter-clockwise while going forward.
  * `arc-right` - issues a 450 turn clockwise while going forward.
  * `pivot-left` - issues a 900 turn counter-clockwise.
  * `pivot-right` - issues a 900 turn clockwise.
  * `stop` - issues an immediate stop.  

**<a name="BOTVACattr"></a>Attributes**

* <a name="actionInterval"></a>`actionInterval`  
  time in seconds between status requests while Device is working
* <a name="boundaries"></a>`boundaries`  
  Boundary entries separated by space in JSON format, e.g.  
  `{"type":"polyline","vertices":[[0.710,0.6217],[0.710,0.6923]],"name":"Bad","color":"#E54B1C","enabled":true}`  
  `{"type":"polyline","vertices":[[0.7139,0.4101],[0.7135,0.4282],[0.4326,0.3322],[0.4326,0.2533],[0.3931,0.2533],[0.3931,0.3426],[0.7452,0.4637],[0.7617,0.4196]],"name":"Kueche","color":"#000000","enabled":true}`  
  [Description of syntax](https://developers.neatorobotics.com/api/robot-remote-protocol/maps)  
  The value of paramter `name` is used as setListe for `setBoundariesOnFloorplan_<floor plan>`.
  It is also possible to save more than one boundary with the same name.
  The command `setBoundariesOnFloorplan_<floor plan> <name>` sends all boundary with the same name.

</ul>
