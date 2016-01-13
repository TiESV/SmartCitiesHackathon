#Clean Water Access in Ethiopia
 
##Why Water Access
 
The World Economic Forum announced this year that the water crisis is the #1 global risk based on impact to society. Over 700 million people are suffering from lack of access to clean, safe water.
 
Women and girls especially (like the one shown in the picture) bear the burden of walking miles at a time to gather water from streams and ponds – full of water-borne disease that is making them and their families sick.
 
Illness from drinking dirty water and the time lost in fetching it robs entire communities of their future.

![Sample Water Image](https://github.com/TiESV/SmartCitiesHackathon/blob/master/watermanagement/water.png)
 
##Theme Overview

###Set Up
This hackathon game is set up in Ethiopia, where most residents do not have piped water access. The following actors and resources are in play:

#####Residents:
2,500 residents who need to obtain 125 liters of water each day for their families. Residents have a small monthly budget to buy water.

#####Water sources:
* 10 public water standpipes
* 3 wells equipped with hand pumps
* 10 household water resellers – households who have piped water supply and sell piped water to their neighbors
* 15 mobile water vendors – vendors who transport and sell water to residents’ homes

#####NGO:
A not-for-profit organization with the mission of improving clean water access

###The Developer’s Role
As a developer, you play the role of the NGO in this game. Your goal is to maximize the number of residents who can have clean water access each day. You have a budget of $125 to manage, and a number of means of intervention to achieve this goal.
 
Your game score is determined by the total number of person days residents have access to water. It will be one of the main factors in evaluating your hackathon performance.
 
###The Rhythm

The game activities run on a simulated daily cycles according to an artificial clock with or without your intervention. You will get notification on very tick. Each Tick of Virtual Clock is equivalent to 1 Minute of Virtual Time. You will receive Ticks very 2000ms (2s) in real-time. Therefore one day in the game is equivalent to 48 minutes in real time.
 
##How It Works

###The Main Character

The main character in this game is the resident.

#####Water Sources
Each day every resident will attempt to obtain water from one of the multiple water sources. Each of the water sources carries different costs and risks.

#####Decision Making
The residents always follow the guidance from the NGO. As the developer, you are the NGO who will provide this guidance on a daily basis to each resident. You must provide this information before 10 AM every day, because the residents make their decisions at 10 AM.
 
If your guidance arrives after 10 AM, it will become the decision source for the resident on the following day. If you fail to provide any guidance, the resident will go to a default location set by the game.
 
The residents who failed to get water in the first attempt may have a second opportunity to go to one of the household resellers who also operate at an off-hour schedule, at 8 PM. You can provide this alternative guidance before 5 PM to such residents.

#####Budget
Each resident has a fixed amount of income allocated for water: $4.50 each month. Residents acquire their monthly budget for the month on the first day of the current month at 6 AM.
 
You *(the NGO)* can decide to directly subsidize any resident using your budget (DaySubsidy). Any subsidies you give will be added to the resident’s budget at 6 AM.

#####Costs
The costs to the residents of obtaining water involve not just the water price itself:
 
**The price of water:** only the well water is free. Standpipes *($1.63 per cubic meter)*, household resellers *(ranges from $1.50 ~ $4.00 per cubic meter)* and mobile vendors *(ranges from $3.50 ~ $4.50 per cubic meter)* provide at at different price rates.
 
**The cost of time:** = *(TravelTime + WaitTime) x HourCost*, where TravelTime is the time it takes to walk from home to the water source; WaitTime is the time waiting in queue, and HourCost is the opportunity cost of time for the resident *($0.10 per hour)*
 
**Health Cost:** if the resident obtains contaminated water, the family will get sick. A HealthCost of $1.50 will be deducted from the resident’s water budget if this happens.
 
###A Typical Day

#####6 AM
The residents’ budgets are updated

#####6 AM – 10 AM
The developer (NGO) sends to residents the water source guide for the day

#####10 AM
The residents read the water source guide and decide to go.

#####10 AM – 12 NOON
Residents’ water source destinations are published to the water sources.

#####12 NOON
Each water source calculates and updates operational parameters, such as queue length, wait time, pump condition, and max capacity. Each water source will reject customers (residents) who fall beyond its max capacity of the day.

#####2 PM
Residents get water and incur all costs.

#####2 PM – 8 PM
The developer (NGO) provides alternative water source guidance (of household resellers) to residents who failed to get water

#####8 PM
The household resellers sell water on off-hour operations
 
###Other Resources – Standpipes
 
The standpipes are shared water pipe outlets in public locations to provide (sell) water to residents. They have fixed locations.

#####Water price (UnitPrice)
$1.63 per cubic meter

#####Flow rate
The flow rate is the main determinant of the queue length and the max capacity of the standpipes. Flow rate is determined by pipe diameters and water pressure. Each standpipe has an *ExpectedPressure*, ranging from 50 ~ 70 kPa. However, the actual pressure may be lower than the *ExpectedPressure* on any given day due to several reasons:

1. The pipe is leaking
2. Water theft
Instrumenting *PressureSensor* is the way for the developer to monitor the standpipe pressure, detect potential problems and intervene. For example, applying maintenance can fix leaking problems and restore the pipe pressure to its *ExpectedPressure*.

#####Tap Condition
The taps of the standpipe may get worn and broken. Once it happens, its condition will transition from *normal to impair to broken*. Water is still accessible from a standpipe when the tab is impaired, but not when it is *broken*. Once a tap is *impaired*, it will be *broken* after 3 days. An impaired or broken tap can be restored to normal by the developer applying maintenance.

#####Water Meter and Vandalism
The standpipes have water meters. An automated meter reading (AMR) system provides the water meter reading. Sometimes vandalism happens at the standpipes that will result in broken meters. Water is not accessible at standpipes with broken meters. Developers can restore broken meters by applying maintenance.

#####Staffing
The developer can pay for staffing that the standpipes. Staffing will have the following impact:

1. Develop will get notified of impaired tap condition;
2. The mean wait time for a given queue is reduced and daily capacity is increased;
3. Water theft can be prevented;
4. One in two vandalism can be prevented.
 
Staffing cost at one standpipe is $______ per day

#####Maintenance
Maintenance can restore all standpipe conditions to normal, including:

1. Pressure and flow rate
2. Tap condition
3. Water meter
 
 
Each one-off maintenance costs $______. It can be applied at any time by the developer. Each scheduled maintenance costs $_______. It can be set by the developer to repeat at any time interval.
 
###Other Resources – Wells
 
Wells are a main alternative source to piped water. With urbanization and population growth, many African cities see higher percentage of residents obtaining water from wells.

#####Price
Water obtained from wells is free

#####Drilling Wells
In addition to the 3 wells provided by the system, the developer as the NGO can drill wells in selected locations. A well with the necessary hand pump will cost the NGO $____ one time cost. The developer needs to provide the location of the well. Locating the well in strategic locations will help more residents get access to water.

#####Flow Rate
The flow rate is the main determinant of the queue length and the max capacity of the wells. Each well has a maximum flow rate *(MaxFlowRate)*. The actual flow rate may be lower than the maximum due to chemical encrustation that happens over time. Maintenance can remove the encrustation and restore the flow rate to maximum level.

#####Pump Condition and Metering
The hand pump at each well has wearing and tearing. Its condition deteriorates over time, until it becomes broken. The developer will only know the pump is broken by the time no water is supplied from the well, based on the water meter reading. The water meter can be installed at a cost of $____ to the NGO.

#####Contamination and the EColiSensor
On some days, some well water may be contaminated. Contaminated water has various risks of causing residents to be sick depending on its bacteria concentration (the higher the concentration, the higher the risk). Sick residents will incur Health Cost. The developer should direct residents away from wells on days when the water is contaminated.
 
The developer can monitor contamination by installing EColiSensor in the well. It costs $_____ per well, one time. The EColiSensor will send the developer periodical updates of its reading. The EColiSensor does not detect low level of bacteria, but can detect anything above 103 CFU/ml.

#####Maintenance
Maintenance can restore all well and hand pump conditions to normal, including:
 
1. Restore to maximum flow rate
2. Restore hand pump condition to perfect
3. Fix broken water meters
 
Each one-off maintenance costs $______. It can be applied at any time by the developer. Each scheduled maintenance costs $_______. It can be set by the developer to repeat at any time interval.
 
###Other Resources – Household Resellers
 
Household resellers play a major role in the informal water market. These households have piped water connections, and decide to resell water to often neighbors who do not have pipe connections. Often they have a yard tap from which they provide and sell water.

#####Price
Water sold by household resellers may costs anywhere between $1.50 ~ $4.00 per cubic meter. This price may vary based on the demand (the more residents getting water from the household, the higher the price).

#####Flow Rate
The flow rate is the main determinant of the queue length and the max capacity at the household reseller. This rate is stable and does not change for household resellers.

#####Off hour sales
Situated in the neighborhood, the household resellers have the flexibility of providing water at late hours. They run a second off-hour operation at 8 PM each day. Residents who did not get water during the day can have an opportunity to obtain water from one of the household resellers. The developer needs to provide the source guidance to such residents.
 
###Other Resources – Mobile Vendors
 
Mobile vendors play the role of covering distant areas on the borders of the cities where other sources of water is far to reach. Buying water from mobile vendors will avoid travel and wait time

#####Price
Ranges from $3.50 ~ $4.50 per cubic meter

#####GeoCoverage
Each mobile vendor has a coverage area. Only residents living within the coverage area have the option of obtaining water from the mobile vendor.

#####Theft Tendency
Some mobile vendors tend to steal water and sell.  If they steal water, one or more of the standpipes may be compromised.

#####Contamination
On some days, some mobile vendor’s water may be contaminated. Contaminated water has various risks of causing residents to be sick depending on its bacteria concentration *(the higher the concentration, the higher the risk)*. Sick residents will incur Health Cost. The developer should direct residents away from mobile vendors on days when the water is contaminated.

#####Certification
The developer can certify the mobile vendors. Certification has the following effects:

1. Certified vendor will not steal water. Some uncertified vendor may steal water.
2. Certified vendor will measure and report EColiSensor data every day, which is used to monitor contamination. Uncertified vendors will not report EColiSensor data.
 
The certification program costs NGO $_____ to initiate, and $______ per day to run. The program will convert more and more mobile vendors to be certified each day. The developer has to initiate the program. If the developer stops the certification program in the middle, all certified vendors would become uncertified.
 
## The Developer’s Guide
This section contains three parts.  Part 1 describes the models running in the system and their attributes. Part 2 describes the queries, subscriptions or notifications available to you. Part 3 describes the actions/interventions you can take via your app to optimize the NGO’s performance results.
### Part 1. Models and attributes

|Models and attributes|Descriptions|
|--------|--------|
|***Resident***||
|ResidentID|Each resident’s unique ID. Example|
|Name|Name of the Resident|
|BudgetBalance|The current water budget the resident has, updated daily|
|MonthlyAllowance|Monthly amount received for the resident to fetch water|
|DaySubsidy|Per day subsidy received for the resident
|SourceGuideID|Water Source Guide ID|
|WaterSourceID|Water Source ID|
|WaterNeed|Amount of Water needed based on family need|
|WaterAccess|Does Resident have access to water for the day?|
|DaysOfAccess|Number of days Resident had Water Access|
|SourceType|Water Source Type – Wells, Stand Pipes Mobile Vendors, Household Resellers|
|HouseLocation|The geo-coordinates of the resident’s house location|
|UnitCost|Unit cost of water|
|TravelTime|Time required to travel for water|
|TravelDistance|Distance required to travel for water|
|WaitTime|Wait time to fetch water|
|HourCost|Hourly cost to fetch water|
|WaterCost|Cost for water|
|HealthCost|Cost incurred due to health issues due to contaminated water received|
|Mobile|Mobile number of the Resident|
|Contamination|Was the water received contaminated?
|***Standpipe***||
|SourceType|Water Source Type. In this case it is StandPipe|
|Name|Name of the Stand Pipe|
|WaterSourceID|Unique Water Source ID assigned to each Stand Pipe|
|GeoLocation|Geo Location of the Stand Pipe|
|OperatingHours<br/><br/>UnitPrice|Hours of operation of the Stand Pipe<br/><br/>Unit Price of Water at this Stand Pipe|
|QueueSize|Current queue size at this Stand Pipe|
|ExpectedPressure|Expected Pressure at this Stand Pipe|
|EffectivePressure|Effective Pressure at this Stand Pipe|
|WaitTime|Wait Time at this Stand Pipe|
|Attendant|Is there an Attendant at this Stand Pipe?|
|WaterSold|Quantity of Water Sold|
|WaterRevenue|Revenue generated from this Stand Pipe|
|PressureSonsorId|ID of the Pressure Sensor that is installed at the Stand Pipe|
|AMR|Cumulative Meter Reading|
|CustomerCount|Current count of the customer at this Stand Pipe|
|Metered|Is the Stand Pipe metered?|
|Instrumented|Is the Stand Pipe Instrumented?|
|***Well***||
|Name|Name of the Well|
|SourceType|Water Source type. In this case it s “Well”|
|WaterSourceID|Unique Source ID assigned to each Well.|
|MaxFlowRate|Max Flow Rate of the well|
|GeoLocation|Geo Location of the Well|
|Metered|Is the Well Metered?|
|QueueSize|Number of people standing to receive water at this Well.|
|PersonTime|Amount of time allocated for a person at this well|
|WaitTime|Average wait time to receive water at this well.|
|Instrumented|Is the well instrumented?|
|EcoliSensorId<br/><br/>WaterMeterId|Is there an Ecoli Sensor installed at this well?<br/><br/>Unique ID of the Water Meter installed at this well.|
|WaterRevenue|Revenue generated from this Well|
|Attendant<br/><br/>CustomerCount|Is there an Attendant at this Well?<br/><br/>Current count of the customer at this Well|
|***Household reseller***||
|SourceType|Water Source Type. In this case it is “Household Reseller”|
|Name|Name of the Household reseller|
|WaterSourceID|Unique Source ID assigned to each household reseller|
|GeoLocation|Geo Location of the Household reseller|
|UnitPrice|Unit price of water at this household reseller|
|WaterSold|Amount of Water Sold by this household reseller|
|WaterRevenue|Revenue generated by this household reseller|
|QueueSize|Number of people standing to receive water from this household reseller|
|WaitTime|Average wait time to receive water from this household reseller.|
|***Mobile vendor***||
|Name|Name of the Mobile Vendor|
|SourceType|Water Source Type. In this case it is “Mobile Vendor”|
|WaterSourceID|Unique Source ID assigned to each Mobile Vendor|
|GeoLocation|Geo Location of the Mobile Vendor|
|Radius|Radius covered by the Mobile Vendor|
|GeoCoverage|Geo Coverage covered by the Mobile Vendor|
|UnitPrice|Unit price of water from this Mobile Vendor|
|MaxCapacity|Maximum Capacity at which water flows at this Mobile Vendor|
|Certified|Is the Mobile Vendor Certified?|
|WaterSold|Amount of Water sold by this Mobile Vendor|
|WaterRevenue|Revenue generate by this Mobile Vendor|
|EcoliSensor|Is there an Ecoli Sensor installed at this Mobile Vendor Location?|
|***NGO***||
|StartingBudget|Starting Budget Allocated for NGO|
|BudgetBalance|Remaining Balance for NGO|
|CertificationProgram|Is there a certification program that NGO is enrolled in?|
 
 
###Part 2. What information you have and how

## Before you run the queries:

 - Please note that you need to initialize the data before your run the queries using "initialize" query from the TQLStudio Query Editor. Please refer to your OnBoarding document on how to Login to TQLStudio and access various queries.
 - Start the Simulation using StartExecution Query.
 - Stop the Simulation using StopExecution Query.
 - 
### Make sure to run queries over HTTP Endpoint and not Websocket.

||Descriptions and API|
|--------|--------|
||***Residents related***|
|1|Query the HouseLocation, Mobile number, WaterNeed, the current budget level of each resident<br/><br/>*Query the Residents Model. There are 1200 residents in total. You can get data for all 1200 Residents using following query. Note that there are 1200 Residents in total. Each Resident is named as Resident-1, Resident-2, …Resident-1200*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular Resident (say – Resident-80) by name simply replace*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/><br/>with<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”Resident-80”&gt;**<br/><br/>*Response Contains all the parameters listed in the Residents Model above. HouseLocation, Mobile Number and WaterNeed are part of the model.*<br/><br/>**Sample Response:**<br/><br/>&lt;Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Id&gt;KHFUC422AAAAUAABAMKRN3LJ&lt;/Id&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;TravelDistance/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SourceGuideID/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;HouseLocation&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;latitude&gt;8.3232133510&lt;/latitude&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;longitude&gt;36.8234050200&lt;/longitude&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/HouseLocation&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaitTime/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;HealthCost/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;DaySubsidy/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;HourCost/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;RecordDate/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Mobile/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterAccess/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Contamination&gt;false&lt;/Contamination&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterCost/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;UnitCost/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;MonthlyAllowance&gt;4.5000000000&lt;/MonthlyAllowance&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ResidentID/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;TravelTime/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterSourceID/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;BudgetBalance/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SourceType/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterNeed&gt;125.0000000000&lt;/WaterNeed&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Name&gt;Resident-84&lt;/Name&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;DaysOfAccess&gt;0&lt;/DaysOfAccess&gt;<br/> &lt;/Residents&gt;|
|2|Query the residents’ current BudgetBalance, WaterSourceID, WaterAccess on any particular day<br/><br/>*Query the Residents Model. There are 1200 residents in total. You can get data for all 1200 Residents using following query. Note that there are 1200 Residents in total. Each Resident is named as Resident-1, Resident-2, …Resident-1200*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular Resident (say – Resident-80) by name simply replace*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/><br/>with<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”Resident-80”&gt;**<br/><br/>*Response contains all the parameters listed in the Residents Model. BudgetBalance, WaterSourceID, WaterAccess are part of the list.*<br/><br/>Please note that the attribute values are updated as per following rules:<br/>*WaterSourceID – Gets updated based on Macro Call: decideSource1.*<br/>*BudgetBalance – Gets updated in many ways (addAllowance, addSubsidy, getWater)*<br/>*WaterAccess – Updated to true or false (If Resident gets the water from suggested WaterSourceID it is set to True; else false)*|
|3|Query the residents’ DaysOfAccess<br/><br/>*Query all the residents DaysOfAccess.*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular Resident (say – Resident-80) by name simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”Resident-80”&gt;**<br/><br/>*Response contains all the parameters listed in the Residents Model. DaysOfAccess is part of the list.*<br/><br/>*Please note that Everyday Resident get water DaysofAccess is incremented by*<br/>1.|
|4|Query the residents’ UnitCost, the water price he/she paid on a particular day, TravelTime, WaitTime, HourCost, WaterCost and HealthCost.<br/><br/>*WaterCost: the total cost of obtaining water on a particular day.<br/>WaterCost = UnitCost × WaterNeed + (TravelTime + WaitTime) × HourCost*<br/>*HealthCost= $1.50 every time the resident gets sick*<br/><br/>*Query all the residents’ information.*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Residents&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular Resident (say – Resident-80) by name simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”Resident-80”&gt;**<br/><br/>*Response contains all the parameters listed in the Residents Model. UnitCost, TravelTime, WaitTime, HourCost is part of the list.* <br/><br/>Based on suggested WaterSourceID following attributes are updated on a daily basis.<br/><br/>- TravelTime<br/>- WaitTime<br/>- HourCost<br/>- WaterCost<br/>- HealthCost<br/>- UnitCost<br/>- TravelDistance<br/><br/>*It is developer’s responsibility to store historical information for future analysis and statistics.*|
||***Standpipes related***|
|5|Query the SourceType, WaterSourceID, and GeoLocation of all the water sources<br/></br/>*Query all the Standpipes in the system. Note that there are three Standpipes in the System and each StandPipe is named as StandPost-1, StandPost-2, StandPost-3*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model above. SourceType, WaterSourceID and GeoLocation are part of the Response.*<br/><br/>**Sample Response:**<br/><br/>&lt;Standpipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Id&gt;KHFZ6P3PAAAAUAABAP7BKDP6&lt;/Id&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Contamination&gt;false&lt;/Contamination&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;EffectivePressure/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;GeoLocation&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;latitude&gt;8.3590645200&lt;/latitude&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;longitude&gt;36.8452087000&lt;/longitude&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/GeoLocation&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Name&gt;StandPost-3&lt;/Name&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Attendant&gt;false&lt;/Attendant&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;QueueSize/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;ExpectedPressure&gt;60.0000000000&lt;/ExpectedPressure&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterRevenue/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;PressureSensorId/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;SourceType&gt;Standpipe&lt;/SourceType&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterSold/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;UnitPrice&gt;1.6300000000&lt;/UnitPrice&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;RecordDate/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;AMR/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Metered&gt;false&lt;/Metered&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterSourceID&gt;WS456&lt;/WaterSourceID&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;WaitTime/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Instrumented&gt;false&lt;/Instrumented&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;CustomerCount/&gt;<br/> &lt;/Standpipe&gt;|
|6|Query the OperatingHour and the UnitPrice of the standpipes<br/><br/>*Query the standpipes in the system.*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model. OperatingHour and UnitPrice are part of the response.*|
|7|Standpipe tap status notifications. The tap condition will go from “normal” à “impaired” à “broken”. The developer will receive notifications on the following situations:<br/>a. Whenever a tap becomes “broken”, the developer will receive a notification;<br/>b. On each day when the tap stays in “broken” state, the developer will receive a notification;<br/>c. Whenever a tap changes from “broken” to “normal”, or “impaired” to “normal”, due to maintenance, the developer will receive a notification of such change<br/>d. IF the standpipe is staffed, then whenever a tap becomes “impaired”, the developer will receive a notification (because the staff will report it);<br/>e. **IF** the standpipe is staffed, on each day when the tap stays in “impaired” state, the developer will receive a notification.<br/><br/>The developer will NOT receive notifications when:<br/>a. The tap is “normal”<br/>b. The tap changes from “normal” to “impaired”, but the standpipe is NOT staffed<br/>c. The tap is “impaired”, but the standpipe is NOT staffed<br/><br/>*Tap Condition for StandPipe is published on WaterSourceStatus Model. In order to receive notifications about TapCondition, you need to issue a TQLSubscription request over the WebSocket EndPoint. You can access the WebSocket EndPoint URL from your Query Tab of TQLStudio.*<br/><br/>**Subscription Request To WaterSourceStatus:**<br/><br/>&lt;Query Storage='TqlSubscription'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Save&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;TqlSubscription Label=”StandPipeTapCondition” sid='20'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Topic&gt;*watermanagement.distribution.WaterSourceStatus.*&lt;/Topic&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/TqlSubscription&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Save&gt;<br/> &lt;/Query&gt;<br/><br/>*You will see responses published on the WebSocket Listener whenever the TapCondition changes based on flow described above. TapCondition is the Name of the Attribute to look for.*<br/><br/>- Automatically received only if broken.<br/>- If Attendant is hired then impaired notifications are published as well.|
|8|Query the ExpectedPressure of standpipes<br/><br/>*Query the standpipes in the system.*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model. ExpectedPressure is part of the response.*|
|9|**IF** the standpipe is staffed, can query the WaitTime of the standpipe, which is the median wait time on a particular day<br/><br/>*Query the standpipes in the system.*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne =””/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply change*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Id ne “”/&gt;<br/><br/>To<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model. WaitTime is part of the response. WaitTime is updated on a dailybasis.*|
|10|Query the “Attendant” value of standpipes – whether the standpipe is staffed<br/><br/>*Query the standpipes in the system which has Attendants*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt; Attendant eq =”True”/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply add*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt**;<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Attendant eq=“True”/&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model. Attendant is part of the response. If there is NO attendant the response contains:*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Find Status="NoResult"/&gt;|
|11|Query the “Instrumented” value of standpipes – whether the pressure sensor is in place<br/><br/>*Query the standpipes in the system which is Instrumented*<br/><br/>&lt;Query&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Find&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipe&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Instrumented eq =”True”/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/StandPipe&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;/Find&gt;<br/> &lt;/Query&gt;<br/><br/>*In order to Query a particular StandPipe by name (say, StandPost-1) simply add*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Name eq=”StandPost-1”&gt;**<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;**&lt;Instrumented eq=“True”/&gt;**<br/><br/>*Response contains all the parameters listed in the StandPipe Model. Instrumented is part of the response. If there is NO StandPipes that are instrumented the response contains:*<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Find Status="NoResult"/&gt;|
|12|**IF** the developer has instrumented pressure sensors on standpipes, he/she can receive the PressureSensor readings from the standpipes that are instrumented *(The PressureSensor reading should be equal to the EffectivePressure of the standpipe at the time)*. For the one’s instrumented, they will receive at a frequency of every 10 seconds, or every 1 hour of game time<br/><br/>*In order to Instrument Pressure Sensor, invoke buyPressureSensor Macro. Once purchased this will monitor the pressure level of the standpipe. One time cost will be deducted from the NGO balance for purchasing the pressure sensor.*<br/><br/>&lt;buyPressureSensor&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipeName&gt;StandPost-1&lt;/StandPipeName&gt;<br/>&lt;/buyPressureSensor&gt;<br/><br/>*Once Instrumented, you will start receiving notifications over websocket if you have already subscribed to WaterSourceStatus Model. The name of the attribute to look for is EffectivePressure.*<br/><br/>*In order to receive notifications about EffectivePressure, you need to issue a TQLSubscription request over the WebSocket EndPoint. You can access the WebSocket EndPoint URL from your Query Tab of TQLStudio.*<br/><br/>**Subscription Request To WaterSourceStatus:**<br/><br/>&lt;Query Storage='TqlSubscription'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Save&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;TqlSubscription Label=”StandPipeTapCondition” sid='20'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Topic&gt;*watermanagement.distribution.WaterSourceStatus.*&lt;/Topic&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/TqlSubscription&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Save&gt;<br/> &lt;/Query&gt;<br/><br/>*You will see responses published on the WebSocket Listener whenever the TapCondition changes based on flow described above. EffectivePressure is the Name of the Attribute to look for.*|
|13|Query the WaterSold value of standpipes<br/><br/>*Code/Queries/Macro, etc*<br/><br/>*Straightforward query.*|
|14|Receive the AMR value from the standpipes. The developer will receive the AMR *(meter reading)* from each standpipe at 12 midnight. The AMR is the cumulative reading of all the water flown through the standpipe<br/><br/>*Code/Queries/Macro, etc*<br/>*AMR – Purchase-only attribute;*<br/>*MeterReading holds cumulative ready. Developer (?)*|
|15|Receive notification regarding the meter condition of the standpipes in the following situations:<br/><br/>a. When the MeterCondition becomes “broken” for any standpipe;<br/>b. For each day when the MeterCondition remains “broken”, the developer will receive notification.<br/>c. When the MeterCondition changes from “broken” to “normal” via maintenance<br/><br/>The developer will not receive notification when the MeterCondition remains “normal”.<br/><br/>*Instrument Water Meter:*<br/>*Description:* The macro deals with the buying a water meter, which will be checking the consumption of water from a particular standpipe at the Stand post.One time cost has been deducted from the NGO balance equal to the water meter Cost.<br/><br/>&lt;buyWaterMeter&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandPipeName&gt;StandPipe-1&lt;/StandPipeName&gt;<br/>&lt;/buyWaterMeter&gt;<br/><br/>*notification :*<br/>*MeterReading*<br/>*MeterCondition*| 
||***Well related***|
|16|**IF** the developer has installed WaterMeter, he/she will receive meter reading, everyday for each well with meter at 12 midnight. The water meter reading is the cumulative reading of all the water flown through the hand pump<br/><br/>*Code/Queries/Macro, etc*<br/><br/> &lt;buyWellWaterMeter&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/buyWellWaterMeter&gt;<br/><br/>*notification :*<br/>*MeterReading*<br/>*MeterCondition*|
|17|Receive notification regarding the MeterCondition when:<br/>a. When the MeterCondition of any well changes from “normal” to “broken”<br/>b. For each day when the MeterCondition remains “broken”<br/><br/>&lt;buyWellWaterMeter&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/ buyWellWaterMeter&gt;<br/><br/>*notification :*<br/>*MeterReading*<br/>*MeterCondition*|
|18|Query if a well is Metered or not. Query if a well has EColiSensor instrumented or not<br/><br/>*Straight Query: Look for Instrumented value; updated only if purchased.*<br/><br/>&lt;buyWellEColiSensor&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/buyWellEColiSensor&gt;<br/><br/>*Look for Metered; updated only if purchased.*<br/><br/>&lt;buyWellWaterMeter&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/buyWellWaterMeter&gt;|
|19|**IF** the developer has instrumented E. Coli sensor on any well, he/she will receive sensor reading *(the EColiSensor value)* every hour *(game time, 24 times a day)* from those wells.<br/><br/>*Install EcoliSensor*<br/>**Description:** The macro deals with the buying a EcoliSensor for Well which will be checking the contamination level of the water at Well. One time cost has been deducted from the NGO balance equal to the EcoliSensor Cost.<br/>&lt;buyWellEColiSensor&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellId&gt;Well -1&lt;/ WellId&gt;<br/>&lt;/buyWellEColiSensor&gt;|
||***Household resellers related***|
|20|Query the UnitPrice of the household resellers<br/><br/>*Straight Query.*|
||***Mobile vendors related***|
|21|Query the GeoCoverage, UnitPrice and MaxCapaccity of the mobile vendor<br/><br/>*Straight Query.*|
|22|Query the “Certified” status of the mobile vendor. Query how many mobile vendors are “Certified”<br/><br/>*Straight Query.*|
|23|Query WaterSold and WaterRevenue value of the mobile vendor<br/><br/>*Straight Query.*|
|24|Receive EColiSensor data from certified vendors (only) at 6 AM every day. If a vendor’s Certified value is “no”, the developer will not receive the EColiSesnor data.<br/><br/>*Notification is received only if vendor is Certified. They have to start the Certification program at cost.*<br/><br/>&lt;turnOnNGOCertification&gt;<br/>&lt;/turnOnNGOCertification&gt;|
||***NGO related***|
|25|Query the StartingBudget and BudgetBalance<br/><br/>*Straight Query.*|
|26|Query if the CertificationProgram is “on” or “off”<br/><br/>*Straight Query.*|
||***Other***|
|27|Subscribe to or query the artificial clock time<br/><br/>*WaterManagement Simulator provides access to Virtual Clock running within the System.*<br/><br/>*Please use WebSocket Connection EndPoint for Subscription and Notification.*<br/><br/>**Subscribe To the Clock**<br/>&lt;Query Storage='TqlSubscription'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Save&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;TqlSubscription Label='TiEClock' sid='11'&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;Topic&gt;*watermanagement.distribution.VirtualClock.*&lt;/Topic&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/TqlSubscription&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Save&gt;<br/> &lt;/Query&gt;<br/><br/>**You will get Notifications over Websocket as follows:**<br/>&lt;TqlNotification&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;Update&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;KHDLSVF6AAAAUAABAPTNJVOI&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;watermanagement.distribution.VirtualClock.CurrentDate Value="" OldValue="" Known="2012-12-13T08:05:02Z" OldKnown="1355414702000" Version="1" Timestamp="1450738596212"/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;watermanagement.distribution.VirtualClock.CurrentHour Value="" OldValue="" Known="20" OldKnown="19" Version="1" Timestamp="1450738596212"/&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/KHDLSVF6AAAAUAABAPTNJVOI&gt;<br/> &nbsp;&nbsp;&nbsp;&nbsp;&lt;/Update&gt;<br/> &lt;/TqlNotification&gt;<br/><br/>. Notifications are received every 4Second Interval. Each 2Second in Real-time represents one 1-Minute on a Virtual Clock.<br/>. The Clock Runs from 0-23 Hours<br/>. The Date increments after 24 Hour Cycle.<br/>.|

###Part 3. What you can do
 
||***Descriptions and API***|
|--------|--------| 
||***Residents related***|
|1|Send residents (each individual resident by Mobile) messages that contain the water source ID they should go to (SourceGuideID). Such messages are only effective if sent at/before 10 AM, because the resident will decide at 10 AM. Messages sent after 10 AM, if not overridden by later messages, will become the decision source for the resident on the following day<br/><br/>*Call this Macro:*<br/><br/>&lt;suggestResidentWaterSource&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;ResidentName&gt;&lt;/ ResidentName&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterSourceID&gt;</ WaterSourceID&gt;<br/>&lt;/suggestResidentWaterSource&gt;<br/><br/>|
|2|Send residents off hour watersource guidance: in case where the residents falls out of the maximum capacity at any of the water sources, the developer can guide residents to go to household resellers at off hours by sending the residents the SourceGuideID before 8 PM on any day.*(the household resellers run another operations at 8 PM)*<br/><br/>*Call this Macro:*<br/><br/>&lt;suggestResidentWaterSource&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;ResidentName&gt;&lt;/ ResidentName&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WaterSourceID&gt;</ WaterSourceID&gt;<br/>&lt;/suggestResidentWaterSource&gt;<br/><br/>|
|3|Give subsidy to any chosen resident of any chosen amount. Can be done any time. Any subsidy given to the resident before 6 AM is accrued on the same day. Any subsidy given to the resident after 6 AM is accrued on the subsequent day. NGO budget will be deducted accordingly by the system<br/><br/>*Grant Subsidy:* The Macro will be Providing Daily Subsidy to the Residents to buy water from the desired water source by adding the subsidy to the Residents Budget and meanwhile deduct the subsidy amount from NGO balance<br/>&lt;grantSubsidy&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;SubsidyAmount&gt;&lt;/SubsidyAmount&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;ResidentName&gt;&lt;/ResidentName&gt;<br/>&lt;/grantSubsidy&gt;|
|4|Schedule a fixed amount of daily subsidy to be given to any chosen resident of any chosen amount. As an example, the condition of given subsidy could be, if any resident’s budget balance falls below $xx. NGO budget will be deducted accordingly by the system<br/><br/>TBD.|
||***Standpipes related***|
|5|Staff any chosen standpipe (Attendant) at any schedule (every day, every other day, every Monday each week, start next month for 15 days, etc.). Remove staff from any chosen standpipe. NGO budget will be deducted accordingly by the system<br/><br/>*Hire Attendant:* The macro deals with the hiring an attendant to monitor the status of the stand pipe whether it is normal or broken. As attendant is hired a specific amount has been deducted from the NGO balance.<br/>&lt;hireStandpipeAttendant&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName &gt;standpipe-1&lt;/StandpipeName&gt;<br/>&lt;/hireStandpipeAttendant&gt;<br/><br/>*Fire Attendant:* The macro deals with removing a attendant from the standpipe.<br/>&lt;fireStandpipeAttendant&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName &gt;StandPipe-1&lt;/StandpipeName&gt;<br/>&lt;/fireStandpipeAttendant&gt;|
|6|Instrument any chosen standpipes (put pressure sensor on them). NGO budget will be deducted accordingly by the system.<br/><br/>&lt;buyPressureSensor&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName&gt;&lt;/ StandpipeName&gt;<br/>&lt;/buyPressureSensor&gt;|
|7|Apply one-off repair and maintenance to any chosen standpipe. NGO budget will be deducted accordingly by the system<br/><br/>*Apply one-off-repair:* The macro simply provide maintenance to the standpipe by enhancing the tap condition. When the macro is executed it will set the tap Condition to Normal, leaking to 0 and meanwhile deduct the maintenance cost from NGO balance<br/>&lt;oneOffRepairMaintenance&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName&gt;Standpipe-1&lt;/StandpipeName&gt;<br/>&lt;/oneOffRepairMaintenance&gt;|
|8|Schedule or cancel/stop regular maintenance for any chosen standpipe. NGO budget will be deducted accordingly by the system<br/><br/>*One-Off-Repair Maintenance:* The Macro Deals with providing Maintenance to the well by repairing and enhancing the pump condition to work it with the maximum frequency. The macro simply raise the flow rate to the maximum and enhance the pump condition and deduct the Maintenance cost from NGO Budget.<br/>&lt;scheduleStandpipeMaintenance&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName&gt;StandPost-1&lt;/StandpipeName&gt;<br/>&lt;/removeScheduleStandpipeMaintenance&gt;<br/><br/>&lt;scheduleStandpipeMaintenance&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;StandpipeName&gt;StandPost-1&lt;/StandpipeName&gt;<br/>&lt;/removeScheduleStandpipeMaintenance&gt;|
||***Well related***|
|9|Choose a location and drill a well. When a well is drilled/created, the developer will be notified (once) of its maximum yield (flow rate), which is randomly assigned to be between 0.28 – 0.48.  NGO budget will be deducted accordingly by the system, including the cost of putting in a hand pump. For the wells that are already in place when the game starts, the developer will NOT know their maximum yield (flow rate)<br/><br/>&lt;digWell&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Name&gt;&lt;/Name&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Lat&gt;&lt;/Lat&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Lon&gt;&lt;/Lon&gt;<br/>&lt;/digWell&gt;<br/>|
|10|Install Water Meter on any chosen well. NGO budget will be deducted accordingly by the system<br/><br/>&lt;buyWellWaterMeter&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;Lon&gt;&lt;WellName&gt;&lt;/WellName&gt;<br/>&lt;/buyWellWaterMeter&gt;|
|11|Instrument E. Coli sensor on any chosen well. NGO budget will be deducted accordingly by the system<br/><br/>&lt;buyWellEColiSensor&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;&lt;/ WellName&gt;<br/>&lt;/buyWellEColiSensor&gt;|
|12|Apply one-off repair and maintenance to any chosen well. NGO budget will be deducted accordingly by the system<br/><br/>&lt;oneOffRepairMaintenanceWell&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;&lt;/ WellName><br/>&lt;/oneOffRepairMaintenanceWell&gt;|
|13|Schedule or cancel/stop regular maintenance for any chosen well. NGO budget will be deducted accordingly by the system<br/><br/>&lt;scheduleWellMaintenance&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/scheduleWellMaintenance&gt;<br/><br/>&lt;removeScheduleWellMaintenance&gt;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&lt;WellName&gt;Well-1&lt;/WellName&gt;<br/>&lt;/removeScheduleWellMaintenance&gt;|
||***Mobile vendors related***|
|14|Start, run and stop certification program (Set CertificationProgram value to “on” or “off”) The developer can start the certification program on any given day. The program will deduct certain budget from the NGO on each day. The developer can stop the certification program at any time.<br/><br/>&lt;turnOnNGOCertification&gt;&lt;/ turnOnNGOCertification&gt;<br/>&lt;turnOffNGOCertification&gt;&lt;/ turnOffNGOCertification&gt;
 
