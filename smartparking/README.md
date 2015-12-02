# Parking Management Use Case

# Introduction
In this game, developers take the role of parking lot operators. The drivers are simulated. This is the only game where multiple developers will be in the same environment. They represent different parking lot operators who may compete or collaborate with each other. Each operator operates 2 parking lots, located in different places.

# Actors

-**Driver**    
-**Parking Lot**      
-**Parking Lot Operator**   
-**Parking Lot Option**   
-**Parking Spot**  
-**Operator App**   
-**City Parking App**  

# Getting Started
To work with the TQL you will need to login into the **TQL Studio**.
Open the following URL in a browser of your choice: schack.tie.org:<port> (You will have to use the port provided to you)
Login credentials are, Username: <email id>, default password: <groupid>
On the home screen you see a tile for "IOT Simulated Apps". Clicking on this will take you to the Apps.
Click on the Parking Management application to open it. 
On the Parking Management screen, you will find a "Queries" tab. 
Clicking on the "Queries" tab will open the editor where you can create, edit and execute queries.
This Screen will also give you the URL to access application as a web service from external application.



# Queries to access the Models:

## Driver:

**Find all Drivers (****Using Find All****)**

```
{
    "Query": {
        "Find": {
            "Driver": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find a Driver by DriverId(***Using where condition***)**

```
{
    "Query": {
        "Find": {
            "Driver": {
                "DriverId": {
                    "eq": "Driver-1"
                }
            }
        }
    }
}
```

**Count the number of Drivers (***Using count***)**

```
{
    "Query": {
        "Find": {
            "Driver": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.Driver.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of Driver(s) at a particular point**

```
{
    "Query": {
        "Find": {
            "Driver": {
                "HomeLocation": {
                    "Latitude": {
                        "eq": " 33.65316654 "
                    },
                    "Longitude": {
                        "eq": "-117.8465224"
                    }
                }
            }
        }
    }
}
```

## ParkingLot

**Find a list of all Parking Lots**

```
{
    "Query": {
        "Find": {
            "ParkingLot": {
                "ParkingLotId": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find a particular Parking Lot**

```
{
    "Query": {
        "Find": {
            "ParkingLot": {
                "Name": {
                    "eq": "UCI Lot 14 - Pereira Dr"
                }
            }
        }
    }
}
```

**Count all Parking Lots**

```
{
    "Query": {
        "Find": {
            "ParkingLot": {
                "ParkingLotId": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value. ParkingLot.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

# API Macros
##### Name:
##### Description:
##### Attribute:
##### Example: 
#

# Querying using http client

URL: [http://sandbox.atomiton.com:9097/fid-parkingmanagement](http://sandbox.atomiton.com:9097/fid-parkingmanagement)

Method: Post

Payload: The desired query, e.g:

```
{
    "Query": {
        "Find": {
            "Driver": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

Result: Output of the Query execution.

# Subscribing through a web-socket

URL: [ws://sandbox.atomiton.com:9097/fid-parkingmanagementws](ws://sandbox.atomiton.com:9099/fid-watermanagementws)

Using a websocket client, connect to the above URL.

The request will look like this:

```
{
    "Query": {
        "Find": {
            "Driver": {
                "Id": {
                    "\_ne": ""
				}    		
			}
		}  
	}
}
```

Sid: is a unique identifier for the Subscription.

Topic: Is the topic to subscribe to, e.g.:

TQL.Update.parkingmanagement.management.Driver.DriverId.\*

TQL.Update.parkingmanagement.management.Driver.\*

TQL.Create.parkingmanagement.management.Driver.\*