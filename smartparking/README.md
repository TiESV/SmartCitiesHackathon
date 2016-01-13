#Parking in the U.S.
##Why Parking

A typical driver spends 106 days of their life searching for parking space. 41% of drivers describe parking as their single biggest automobile “headache”. Very little information is available to the driver on parking availability and price. The pricing mechanisms for parking that exist today are archaic. A driver ends up either paying too much or not enough.

Here you, the developer, will take on the role of a private parking operator with the goal of optimizing revenue by efficient and competitive management of parking spaces and pricing

![Sample Parking Image](https://github.com/TiESV/SmartCitiesHackathon/blob/master/smartparking/parking.png)


##Theme Overview

###Set Up
This hackathon game is set up in the city of _____ in the U.S in an area of city of ____ sq kilometers.  The following actors and resources are in play:

#####Drivers:
1,800 drivers who drive to one destination in town every day and need to find parking spots

#####Resources:
20 parking lots
1 city parking app
#####Parking Lot Operators:
Private operators who run the parking lots.

###The Developer’s Role
As a developer, you play the role of the Parking Lot Operator in this game. You will be assigned 2 parking lots located at different places in the City, each having a capacity of 100 parking spots.
 
Your goal is to maximize revenue by setting the right parking price and attracting more customers (drivers).
 
Your game score is determined by your total revenue. It will be one of the main factors in evaluating your hackathon performance.
 
###The Rhythm
The game activities run on a simulated daily cycles according to an artificial clock with or without your intervention. You will get notification on very tick. Each Tick of Virtual Clock is equivalent to 1 Minute of Virtual Time. You will receive Ticks very 2000ms (2s) in real-time. Therefore one day in the game is equivalent to 48 minutes in real time.
 
##How It Works

###The Main Character
The main character in this game is the drivers.

#####Obtaining Information
The drivers’ parking decisions depend on the information they have of the parking lots. Drivers obtain information from the following three types of sources:
 
1. The City Parking App – this is an app offered by the City. All developers can post parking lot information on it and all drivers can read from it.
2. The Operator Apps – these are the private apps offered by the parking lot operators. Drivers will only get information from an operator app if they choose to adopt the app.
3. Past experience – loyalty
 
 
Most information drivers obtain by “requesting” from the city parking app or operator apps, such as parking lot locations, prices and vacancies. Drivers only request such information when they get close to their destinations. “Close to” is defined as a “DecisionRange” – time to make parking decisions. For each driver
 
```
DecisionR = MIN (1 mile, DistanceCeiling)
```

*Where DistanceCeiling is the maximum distance a driver is willing to park away from his/her final destination.* 

 
The only information drivers receive by "subscription" is parking reservation offers and reservation prices from you, via the operator apps. Every time there is a new offer or update on reservation, they will get it, as long as they have left home and they are using your operator app.

#####Satisfaction and Loyalty
Drivers develop loyalties to you as they (happily) park at your lots day after day. Loyalty pays off in two ways:
1. increase their willingness to park at your lot in future days *(see Making Parking Decisions section)* 
2. increase their likelihood of adopting your operator app *(see Adopt Operator Apps section)*
 
Loyalty is measured by Loyalty Credit, the cumulative sum of Satisfaction scores over all the days when the developer has parked at one of your two lots.

```
Loyalty Credit = Σ (S1, S2, … Sn).
```
*Your reputation as a parking lot operator is the average Loyalty Credit all drivers give you.*
 
Satisfaction is influenced by your price relative to the driver’s PriceCeiling, and by the distance between your lot and his/her destination, relative to the driver’s DistanceCeiling.
 
```
Satisfaction (S) = 100% * √Max [0, ((1- HourlyPrice/PriceCeiling)* (1-ActualDistance/DistanceCeiling))]
```
 
*Where PriceCeiling is the highest hourly rate a driver is willing to pay. DistanceCeiling is the maximum distance a driver is willing to park away from his/her final destination. Both vary across individuals.*
 
On the other hand, if a driver reached your parking lot when it has been fully occupied, he will give a negative satisfaction score S = -5. If a driver made a reservation, went to your lot, and the reserved spot is not available, a negative satisfaction score S = -10 will be given *(see Making Reservation section)*.
 
#####Making Parking Decisions – Utility Functions
Every day, each driver has a destination and start time. The drivers will be choosing which parking lot they go for parking based on their utility functions.
 
**Utility function**: the driver assigns a utility value *(U)* to each parking option he/she is aware of on that day. Usually the option with the greatest *U* value will be chosen.
 
**The following factors determine driver’s _U_ value:**

1. **Reputation** – drivers prefer lots of operators who have better reputations. Your reputation as a parking lot operator is the average Loyalty Credit all drivers give you.
```
Reputation = Σ (Loyalty Credit)/n.
``` 

2. **Assurance of availability** – drivers determine how likely he/she is to find a parking spot at a lot by reading the # of vacancies statistics you provide them. If you fail to provide vacancy information, this assurance will be very low.

3. **Trustworthiness of information** – more trustworthy source of information is weight more.
 
  * If driver’s information comes from your operator app, the *trustworthiness is equal to your OperatorAppRating*.
  * If driver’s information comes from the city parking app, the *trustworthiness T = Average (all OperatorAppRatings)/2*.
  * If driver’s information is from “suggested” lot on an operator app,the _trustworthiness T = 1.5* OperatorAppRating_
 
4. **Distance** – shorter distance between driver’s destination and the parking lot is preferred
 
5. **Cost** – cost equals the hourly price times the parking time needed. Lower cost is preferred
 
**Candidates**: any parking lot must meet two minimum conditions to be considered *(becoming parking Candidates for a driver)*:

1. the hourly rate is within the driver’s PriceCeiling
2. the distance to driver’s destination is within the driver’s DistanceCeiling.
 
**Decision Range**: the driver will not make a decision on the parking lot until he reaches the Decision Range. The Decision Range is a circle around his/her destination with a radius of DecisionR.
```
DecisionR = Min (1 mile, DistanceCeiling).
``` 
Once the driver crosses the Decision Range, he will immediately compare the Candidates available and make a decision for the Candidate with the greatest *U* value.
 
If the driver does not find any Candidates when crossing the Decision Range, he will continue to drive towards the destination, and will choose the **first** qualified Candidate he becomes aware of, either by visually spotting a lot, or via the information just made available on the City Parking App or operator apps, whichever comes first.
 
**Visual spotting**: The driver will spot parking lots within his/her Visual Range. The Visual Range is on the same street as the driver’s *current location* with a distance of *VisualR = 0.2 mile*.
 
*If the driver fails to find a parking lot by the time he reaches his destination, he will by default be routed immediately to the closest parking lot with any vacancies, regardless of price or distance. If the driver reaches a parking lot of his choice, and it turns out to be fully occupied already, he will also be routed immediately to the closest parking lot with any vacancies, regardless of price or distance.*
 
##### Making Reservations
The exception to DecisionRange is reservations. At any time you can offer parking reservations at a special price rate to drivers via your operator app.*This price does not have to be the same as the fixed price of the day and can be changed from time to time on the same day (see Developer’s Guide section for details)*. Drivers subscribe to reservation offer information as soon as he/she leaves home, and until he/she has made a decision. Once a new reservation offer is available, the driver will consider and decide immediately either to take the offer or reject it, *without comparing to any alternative parking options.*
 
The driver will accept the reservation and reservation price if:

1. the parking lot qualifies as a Candidate *(meet PriceCeiling and DistanceCeiling)*
2. he/she calculates the utility function *(U)* of this offer at the reservation price, and it is lower than the *U value of his/her previous day’s choice*.
 
Once the driver decides to get the reservation, you will receive a notification, and must send a vacant spot *#* to the driver as confirmation *(see Developer’s Guide section for details)*.
 
Once confirmed, the transaction is complete and the driver will stop considering other parking lots on that day. When the driver reaches the lot, he/she should be able to park at the designated spot. If the spot number you provided is taken, he/she will give a negative satisfaction score.
 
If the driver rejects a reservation, he/she will not reconsider it later, unless a new reservation price update is made, at which time he/she would re-evaluate it. If a driver rejects a reservation offer, he/she may always decide later to park at the lot without reservation, and at its regular price.
 
 
##### Adopting Operator Apps
Each driver decides which operator app*(s)* to use every day by randomly selecting among the top 5 operator apps ranked by their OperatorAppRating’s. A driver may use more than 1 app on the same day, but not more than 3.
 
The OperatorAppRating is an average value calculated from the value each driver gives to the operator: the OperatorAppValue:
 
```
OperatorAppRating = (Σ (OperatorAppValue from all drivers))/ √n
``` 
*n is the number of drivers.*
 
Each driver gives each operator an OperatorAppValue.

```
OperatorAppValue = Loyalty Credit + Information Credit
```

The Loyalty Credit is as defined in the Satisfaction and Loyalty section. Information Credit is the credit a driver gives you each time he/she uses information provided by your operator app to park at parking lot that is NOT owned by yourself.
 
For example, operator A provides suggestion to driver about operator B’s parking lot, which is closer to the driver’s destination. The driver parked at operator B’s parking lot, and gave B a Loyalty Credit = 0.8. Operator A will receive an Information Credit of 0.8 on that day.
 
*You can only suggest other operator’s parking lot via your own app. The other developer needs to give you permission to share his/her lot information on your app.* 
 
### A Typical Day
 
The parking lot operates from 8 AM to 8 PM. The driver may start from home at a random time on each day.
 
Following are the main process for the driver:
 
 
#### Other Resources – City Parking App
 
The City Parking App is provided by the City. All parking lot operators can post information for all drivers and all other operators to see.

As a parking lot operator, you can send updates to the City Parking app any time at any frequency about your parking lots, but the City Parking App updated only every 15 minutes *(game time)*.
 
The City Parking App contains the following information for each parking lot:
 
* OperatorID
* LotID
* LotLocation
* Current date and time
* Today’s price *(hourly rate)* – if published by the operator
* Current *#* of vacancies – if published by the operator
* The Reputation of the operator
 
*Note that you can only set the price once a day at 8 AM. The day’s price will be fixed, except for reservation prices.*

### Other Resources – Operator App
Each parking lot operator has an "operator app". Drivers selectively adopt operator apps based on the *OperatorAppRating*.
 
The operator app has the following benefits:

1. If a driver uses your app, you will be notified when the driver leaves home with his/her Destination and ParkTime (how long he needs to park)
2. You will receive the driver’s current location when he is driving, at an interval of every *2 minutes*
3. You can suggest to the driver the ideal parking lot based specifically on his/her destination. If the driver use your information, you will receive an Information Credit
4. You can offer reservation price at a different rate from your regular rate of the day. This information will be private. The reservation and payment can be handled through the app.
 
You can publish the following information on your operator app for all app users:
 
**My 2 parking lots:**
OperatorID\*
LotID (of lot 1)\*
LotLocation\*
Date and time\*
Today’s price (hourly rate)
Current # of vacancies
Reservation offered – yes/no
Reservation price (hourly rate)
 
OperatorID\*
LotID (of lot 2)\*
LotLocation\*
Date and time\*
Today’s price (hourly rate)
Current # of vacancies
Reservation offered – yes/no
Reservation price (hourly rate)

_* are required fields_
 
In addition, you can provide one suggested parking lot to each individual app user.*The suggested parking lot can either be one of your own parking lots, or someone else’s parking lot. You will need to get permission from other developers to mutually share their lot information in order to suggest someone else’s lot*.
 
**Suggested parking lot (only one) for**
DriverID\*
OperatorID\*
LotID\*
LotLocation\*
Date and time\*
Today’s price (hourly rate)
Current # of vacancies

_* are required fields_
 
The suggested parking lot may be (and should be) different for different drivers, so such updates must contain DriverID’s.
 
If any field of information about the same LotID is available both from the City Parking app and from your operator app, the latter information always overrides the former.
 
### Other Resources – Parking lot
##### Capacity
Each parking lot has 100 parking spots.
##### Occupancy and Infrared Sensors
Each parking spot has a Spot Status of vacant or occupied. There is an infrared sensor at each spot, which sends you data of the spot status every 5 minutes.*You are responsible in keeping the occupancy and vacancy rate for the parking lot based on the sensor data.*
##### Reservation
A Digital Display at each spot can indicate the reservation status of a parking spot to the drivers. *You are responsible for maintaining the right message on all the Digital Displays*. The display can say "reserved" or "null". Drivers who do not have the reservation will not park at spots that say "reserved" on the display. On the other hand, if you do not update the display after giving out a reservation, others may take the driver’s reserved spot. When a driver picks up his/her car from a reserved parking spot and leaves, the status will automatically change to "null".
 
 
 
 
 
 
## The Developer’s Guide

 
This section contains three parts. Part 1 describes the models running in the system and their attributes. Part 2 describes the queries, subscriptions or notifications available to you. Part 3 describes the actions/interventions you can take via your app to optimize the Waste Management Company’s performance results.
### Part 1. Models and attributes

| Models and attributes | Descriptions |
|--------|--------|
|***<div style="text-align:center">Drivers</div>***|        |
|DriverID|*Unique ID assigned to the Driver*|
|Decision|*Indicates the driver has made a decision about the parking lot*|
|ParkedLotID|*Lot ID where the driver has last parked the vehicle*|
|LastUtilityFunction|*Last Utility value (see above for description)*|
|TimeParked<br/><br/>HomeLocation|*Time the vehicle was last parked<br/><br/>Starting Location of the Driver*|
|***<div style="text-align:center">CityParkingApp</div>***||
|OperatorID<br/><br/>LotID|*ID of the Operator<br/><br/>ID of the Lot for which this City Parking App is made available*|
|LotLocation|*Geo Location of the Lot*|
|LastInfoUpdate|*DateTime when the information was last updated for this City Parking App*|
|TodaysPrice|*Latest price to park vehicles at the parking lot to which this City Parking App is assigned*|
|LastAppUpdate|*DateTime when the app was last updated - (? diff with LastInfoUpdate)*|
|***<div style="text-align:center">OperatorApp</div>***||
|AppID|*Unique ID of the Operator App*|
|OperatorID|*ID of the Operator to whom this Operator App belongs*|
|OperatorAppID|*ID for the operator app*|
|DriverID|*ID of the driver who is using this Operator App (? Can it be more than one DriverID?)*|
|AppRating|*App Ratings*|
|LotID|*ID of the Lot to which this Operator App is applicable*|
|LotLocation|*Lot Location to which this Operator App is applicable (? Do we need it here ?)*|
|ParkingDateAndTime|*DataTime when vehicles can be parked at this (?) lot*|
|TodaysPrice|*Price to park the vehicle at this Parking Lot*|
|CurrentNoOfVacancies|*Number of vacant spots at this Parking Lot*|
|ReservationPrice|*Price to reserve the parking Lot*|
|ReservationOffered|*Does this parking Lot offer reservation?*|
|***<div style="text-align:center">ParkingLot</div>***||
|LotID|*Unique ID of the Parking Lot*|
|OperatorID|*ID of the operator to whom this Parking Lot belongs*|
|LotLocation|*Geo Location of the Parking Lot*|
|DigitalDisplay|*Digital Display information associated with this Parking Lot.*|
|ReservationPrice|*Price to reserve a parking lot*|
|RegisteredVacancy|*Number of registered vacancies*|
|AuthorizedOperator|*Authorized Operator*|
|***<div style="text-align:center">ParkingLotOperator</div>***||
|OperatorID|*Unique ID of the Operator to whom the Parking Lot belongs*|
|OperatorAppID|*ID of the operator App that is associated with this Parking Lot*|
|DayRevenue|*Revenue generated per day*|
|LotOnePrice|*Price of LotOne*|
|LotTwoPrice|*Price of LotTwo*|
|TotalRevenue|*Total Revenue generated by this Parking Lot*|
|AuthorizedOperator|*Authorized operator information for this parking lot*|
 
 
### Part 2. What information you have and how
 

||Descriptions and API|
|--------|--------|
|1|Query all information on the City Parking App posted by all the operators<br/>&lt;Find&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;CityParkingApp&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;ID ne=””/&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;/CityParkingApp&gt;<br/>&lt;/Find&gt;|
|2|Subscribe to any changes of information on the City Parking App<br/>&lt;Query Storage='TqlSubscription'&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Save&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;TqlSubscription Label=”CityParkingApp” sid='20'&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Topic&gt;parkingmanagement.management.CityParkingApp.\*&lt;/Topic&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/TqlSubscription&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Save&gt;<br/>&lt;/Query&gt;| 
|3|**IF** another developer has accepted the developer’s request to share parking lot information,<ol style="list-style-type:lower-alpha"><li>the developers can query each other’s parking lots’ following information: OperatorID, LotID, LotLocation, OperatingStatus, DayPrice, RegisteredVacancy</li></ol>They cannot make any changes<br/>*Step 1: Request to Share and Acceptance.*<br/>OperatorApp query needs to be restricted based on acceptance of Sharing<br/>Parking Lot is shared with following request<br/><br/>&lt;shareParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;UserName&gt;&lt;/UserName&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotId&gt;&lt;/LotId&gt;<br/> &lt;/shareParkingLot&gt;<br/>a.<br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;ParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID Eq=’’ /&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/ParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;Query&gt;<br/>|
|4|**IF** any driver has decided to use the operator’s app on any day, the developer will receive the following information when the driver starts from home:<ol style="list-style-type:lower-alpha"><li>When the driver starts from home, receives: DriverID, HomeLocation, Destination (BT), StartingTime (BT), ParkTime (BT)</li><li>During driving, the developer will receive the driver’s current location every time it updates</li></ol>*Step 1: UseOperatorApp to inform the system that Driver is using the operatorApp.<br/>There has to be notion of SessionKey tied to each developer; and all the variables will be dumped to a model with SessionKey. Subscription will be based on the instance id i.e mapped to SessionKey.*<br/><ul><li>&lt;saveOperatorAppInfo&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;KIVPCXLYAAAAUFAEGEH4OGQC&lt;/OperatorID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotNumber&gt;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/LotNumber&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;CurrentVacancies&gt;123&lt;/CurrentVacancies&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationOffered&gt;true&lt;/ReservationOffered&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationPrice&gt;2000&lt;/ReservationPrice&gt;<br/> &lt;/saveOperatorAppInfo&gt;<br/></li></ul>|
|5|**IF** any driver has decided to use the operator’s app on any day, the developer can query the LastU value of the user*(s)*<br/><br/>*Step 1: UseOperatorApp to inform the system that Driver is using the operatorApp.<br/><br/>There has to be notion of SessionKey tied to each developer; and all the variables will be dumped to a model with SessionKey. Subscription will be based on the instance id i.e mapped to SessionKey.*<ul><li>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Driver&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;DriverID eq=’’/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Driver&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/></li><ul>|
|6|The developer will receive all infrared sensor data of all parking spots in his two parking lots<br/>*ParkingSpot Subscription only to the owner of the lot and to shared developers.*<br/><br/>&lt;Query Storage='TqlSubscription'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Save&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;TqlSubscription Label=”CityParkingApp” sid='20'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Topic&gt;parkingmanagement.management.ParkingSpot.*&lt;/Topic&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/TqlSubscription&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Save&gt;<br/> &lt;/Query&gt;<br/>|
|7|2.     Query all DriverID’s who are driving, at any time *(this will allow the developer to get a sense of demand and demand fluctuation)*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Driver&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Decision eq=’false’/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Driver&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/>|
 
### Part 3. What you can do
 

|| Descriptions and API |
|--------|--------|
|1|Set daily price (hourly rate) for the two parking lots. *Price at each parking lot can only be set once a day at 8 AM (when the parking lots open)*. Developers control this price by updating the LotOnePrice and LotTwoPrice values in the parking lot operator models *before 8 AM*. At 8 AM each day, the current values of LotOnePrice and LotTwoPrice will become the DayPrice of the parking lot.<br/><br/>&lt;updatePriceByParkingLotOperator&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt; KIVPCXLYAAAAUFAEGEH4OGQC &lt;/OperatorID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotOnePrice&gt;1200&lt;/LotOnePrice&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotTwoPrice&gt;500&lt;/LotTwoPrice&gt;<br/> &lt;/updatePriceByParkingLotOperator&gt;<br/>|
|2|Publish/update parking lot information to the City Parking app.<ol style="list-style-type:lower-alpha"><li>When developers send parking lot updates to the City Parking app, the OperatorID, LotID, Lotlocation, and Today’s price information will be directly retrieved from the corresponding attributes in the Parking lot models. The number of vacancies will be retrieved from the "RegisteredVacancy" attribute of the parking lot models.</li><li>The developer can choose NOT to publish price information or provide vacancy information in any updates</li><li>The updates can be made to the City Parking app multiple times a day *(but the price will stay the same)*. The City Parking app refreshes every 15 minutes in game time.</li></ol><br/>&lt;saveParkingLotInfo&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;LotID/&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID/&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;TodaysPrice /&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;CurrentVacancies /&gt;<br/>&lt;/saveParkingLotInfo&gt;|
|3|Publish/update parking lot information to the operator app.<ol style="list-style-type:lower-alpha"><li>When developers send parking lot updates to the operator app, the OperatorID, LotID, Lotlocation, Today’s price, ReservationOffer and ReservationPrice information will be directly retrieved from the corresponding attributes in the Parking lot models. The number of vacancies will be retrieved from the "RegisteredVacancy" attribute of the parking lot models, whether reservation is offered (yes/no), and the reservation price.</li><li>The developer can choose NOT to publish price information or provide vacancy information in any updates. The developer can also choose NOT to offer any reservation.</li><li>In addition, the developer can publish "suggested parking lot" information. In this update the developer must specify a DriverID for each suggested parking lot. Only the app user with the matching DriverID will read corresponding "suggested parking lot" information for himself/herself.*The developer will need to get permission from other developers to mutually share their lot information in order to suggest someone else’s lot. Suggested parking lot information of someone else’s parking lot will be read from that operator’s parking lot model.*</li><li>The updates can be made to the operator app multiple times a day and will be refreshed immediately on the operator app.</li></ol><br/>a.<br/>&lt;saveOperatorAppInfo&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;KIVPCXLYAAAAUFAEGEH4OGQC&lt;/OperatorID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotNumber&gt;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/LotNumber&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;CurrentVacancies&gt;123&lt;/CurrentVacancies&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationOffered&gt;true&lt;/ReservationOffered&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationPrice&gt;2000&lt;/ReservationPrice&gt;<br/> &lt;/saveOperatorAppInfo&gt;<br/><br/>b.<br/>&lt;saveOperatorAppInfo&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;KIVPCXLYAAAAUFAEGEH4OGQC&lt;/OperatorID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotNumber&gt;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/LotNumber&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;CurrentVacancies&gt;123&lt;/CurrentVacancies&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationOffered&gt;false&lt;/ReservationOffered&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ReservationPrice&gt;2000&lt;/ReservationPrice&gt;<br/> &lt;/saveOperatorAppInfo&gt;<br/><br/>c.<br/>&lt;sendPrivateInfoToDriver&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;DriverID&gt;Driver-&nbsp;&nbsp;&nbsp;&nbsp;&lt;/DriverID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotID&gt;UCI Lot AV1 - Arroyo Dr&lt;/LotID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SpotID&gt;UCI Lot AV1 - Arroyo Dr-Spot-100&lt;/SpotID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OfferedPrice&gt;5&lt;/OfferedPrice&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;operatorID&gt;&lt;/ operatorID&gt;<br/> &lt;/sendPrivateInfoToDriver&gt;<br/>|
|4|Request and accept information sharing with another developer<ol style="list-style-type:lower-alpha"><li>Developer can request mutually share parking lot information with any other developer. Once accepted, this share will be mutual</li><li>Once shared, a developer can query each other’s parking lot information but cannot make changes. See previous section for details.</li><ol><br/><br/>a.<br/>Request to share parking lot <br/>&lt;shareParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;UserName&gt;&lt;/UserName&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotId&gt;&lt;/LotId&gt;<br/> &lt;/shareParkingLot&gt;<br/><br/>b.<br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;ParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID Eq=’’ /&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/ParkingLot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;Query&gt;<br/>|
|5|*Step 1: Request to Share and Acceptance.*<br/>Manage and maintain parking lot status: the developer is responsible for updating the RegisteredVacancy information of his/her parking lots. He/she can do so by processing the Infrared sensor data from the parking lots.<br/><br/>&lt;reserveParkingSpot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SpotID&gt;&lt;/SpotID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;&lt;/OperatorID&gt;<br/> &lt;/reserveParkingSpot&gt;<br/>|
|6|Managing reservations:<ol style="list-style-type:lower-alpha"><li>The developer is responsible for updating the ReservationOffer and ReservationPrice information of his/her parking lot models</li><li>The developer offers the reservation by publishing such information to the operator app</li><li>Once any user sends a reservation request via the operator app, the developer must respond within 5 seconds with an empty SpotID to conform the reservation. If the developer does not respond within *5* seconds with a SpotID, the request will be considered rejected</li><li>Once the user accepts the reservation SpotID via the operator app, the developer should update the DigitalDisplay at the corresponding spot of the parking lot to "reserved". *(Otherwise other cars may park at the spot)*</li><li>When the car leaves a reserved spot, it will automatically update the DigitalDisplay to "null". The developer does not have to do this<ol><li>&lt;saveOperatorAppInfo&gt; -- See above</li><li>Same as (a)</li><li>&lt;provideReservation&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;DriverID&gt;Driver-&nbsp;&nbsp;&nbsp;&nbsp;&lt;/DriverID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;KIVPCXLYAAAAUFAEGEH4OGQC&lt;/OperatorID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SpotID&gt;UCI Lot AV1 - Arroyo Dr-Spot-100&lt;/SpotID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;LotID&gt;UCI Lot AV1 - Arroyo Dr&lt;/LotID&gt;<br/> &lt;/provideReservation&gt;<br/></li><li>&lt;reserveParkingSpot&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SpotID&gt;&lt;/SpotID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;OperatorID&gt;&lt;/OperatorID&gt;<br/> &lt;/reserveParkingSpot&gt;<br/></li><li>No Macro. Done automatically.</li></ol></li>
 

