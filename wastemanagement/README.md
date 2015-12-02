# Waste Management Use Case

# Introduction

The problem deals with the waste Management in Sigra,Up,India.The Environment consists of two types of residents. “Good” residents always go to the designated trash bins. “Typical” residents decide where to go based on the personal choice.
All the waste Management is processed by a waste Management company(Role played by developers),containing waste transport vehicle with their workers.
Neighbourhood trash bins located in each community and emptied daily by the waste management vehicle.The waste management company have to make sure that each of the resident must use the trash bins for the waste dumping purpose and educate them to dump the waste effectively.
The Environment also consists of Pedestrians across the area of the game.The pedestrians are randomly moving on the streets. When they are within radius of any street dumping site. 
Pedestrians may choose to take a photo of any residents who are currently there at the same time, with their smart phones and post on a social network platform.

# Actors

-**Resident**    
-**Pedestrians**    
-**Neighbourhood trash bin**   
-**Street Posts**   
-**Street dumping sites**   
-**Waste transport vehicle**   
-**Waste transport worker**   
-**Waste management company (role played by the developer)**   

# Getting Started
To work with the TQL you will need to login into the **TQL Studio**.
Open the following URL in a browser of your choice: schack.tie.org:<port> (You will have to use the port provided to you)
Login credentials are, Username: <email id>, default password: <groupid>
On the home screen you see a tile for "IOT Simulated Apps". Clicking on this will take you to the Apps.
Click on the Waste Management application to open it. 
On the Waste Management screen, you will find a "Queries" tab. 
Clicking on the "Queries" tab will open the editor where you can create, edit and execute queries.
This Screen will also give you the URL to access application as a web service from external application.

# Queries to access the Models:

## Pedestrians:

**Find all Pedestrians (****Using Find All****)**

```
{
    "Query": {
        "Find": {
            "Pedestrian": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find a Pedestrian by Name (****Using where condition****)**

```
{
    "Query": {
        "Find": {
            "Pedestrian": {
                "Name": {
                    "eq": "Pedestrian-1"
                }
            }
        }
    }
}
```

**Count the number of Pedestrians (****Using count****)**

```
{
    "Query": {
        "Find": {
            "Pedestrian": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.Pedestrian.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of Pedestrian(s) at a particular point**

```
{
    "Query": {
        "Find": {
            "Pedestrian": {
                "StartLocation": {
                    "latitude": {
                        "eq": "25.3099937400"
                    },
                    "longitude": {
                        "eq": "82.9870729900"
                    }
                }
            }
        }
    }
}
```

## Residents:

**Find a list of all Residents**

```
{
    "Query": {
        "Find": {
            "Resident": {
                "Id": {
                    "\_ne": ""
                }
            }
        }
    }
}
```

**Find a particular Resident**

```
{
    "Query": {
        "Find": {
            "Resident": {
                "Name": {
                    "eq": "Resident-1"
                }
            }
        }
    }
}
```

**Count all Residents**

```
{
    "Query": {
        "Find": {
            "Resident": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.Resident.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

## StreetBlocks

**Find all Street Blocks**

```
{
    "Query": {
        "Find": {
            "StreetBlock": {
                "Id": {
                    "\_ne": ""
                }
            }
        }
    }
}
```

**Count all StreetBlocks**

```
{
    "Query": {
        "Find": {
            "StreetBlock": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.StreetBlock.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of StreetBlock at a particular point**

```
{
    "Query": {
        "Find": {
            " StreetBlock": {
                " LL": {
                    "latitude": {
                        "eq": "25.3141932"
                    },
                    "longitude": {
                        "eq": "82.98308487"
                    }
                }
            }
        }
    }
}
```

## Trash Bins

**Find all TrashBins:**

```
{
    "Query": {
        "Find": {
            "TrashBin": {
                "Id": {
                    "\_ne": ""
                }
            }
        }
    }
}
```

**Count All Trash bins:**

```
{
    "Query": {
        "Find": {
            "TrashBin": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.TrashBin.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of TrashBin at a particular point**

```
{
    "Query": {
        "Find": {
            "TrashBin": {
                "Loc": {
                    "latitude": {
                        "eq": "25.3141932"
                    },
                    "longitude": {
                        "eq": "82.98308487"
                    }
                }
            }
        }
    }
}
```

## WasteTransport vehicle

**Find all WasteTransport vehicle :**

```
{
    "Query": {
        "Find": {
            "WasteTransportVehicle": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find a WasteTransportVehicle by Name (****Using where condition****)**

```
{
    "Query": {
        "Find": {
            " WasteTransportVehicle ": {
                "Name": {
                    "eq": " WTV-1"
                }
            }
        }
    }
}
```

**Count the number of**  **WasteTransportVehicle** **(****Using count****)**

```
{
    "Query": {
        "Find": {
            " WasteTransportVehicle ": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value. WasteTransportVehicle.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of WasteTransportVehicle (s) at a particular point**

```
{
    "Query": {
        "Find": {
            " WasteTransportVehicle ": {
                " ParkedLocation ": {
                    "latitude": {
                        "eq": " 25.311599 "
                    },
                    "longitude": {
                        "eq": " 82.9849042 "
                    }
                }
            }
        }
    }
}
```

## WasteTransportWorker

**Find all WasteTransportWorker (****Using Find All****)**

```
{
    "Query": {
        "Find": {
            " WasteTransportWorker": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find a WasteTransportWorker by Name (****Using where condition****)**

```
{
    "Query": {
        "Find": {
            " WasteTransportWorker ": {
                "Name": {
                    "eq": " WTW-1"
                }
            }
        }
    }
}
```

**Count the number of**  **WasteTransportWorker** **(****Using count****)**

```
{
    "Query": {
        "Find": {
            " WasteTransportWorker ": {
                "Id": {
                    "ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value. WasteTransportWorker.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**List of WasteTransportWorker (s) at a particular point**

```
{
    "Query": {
        "Find": {
            " WasteTransportWorker ": {
                " CurrentLocation ": {
                    "latitude": {
                        "eq": " 25.31133069 "
                    },
                    "longitude": {
                        "eq": " 82.99034186 "
                    }
                }
            }
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

URL: [http://sandbox.atomiton.com:9098/fid-watermanagement](http://sandbox.atomiton.com:9098/fid-watermanagement)

Method: Post

Payload: The  desired query, e.g:

```
{
    "Query": {
        "Find": {
            "Pedestrian": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

Result: Output of the Query

# Subscribing through a web-socket

URL: [ws://sandbox.atomiton.com:9098/fid-watermanagementws](ws://sandbox.atomiton.com:9099/fid-watermanagementws)

Using a websocket client, connect to the above URL.

The request will look like this:

```
{
    "Query": {
        "Find": {
            "Resident": {
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

TQL.Update.wastemanagement.distribution.Resident.Name.\*

TQL.Update.wastemanagement.distribution. Resident.\*

TQL.Create.wastemanagement.distribution. Resident.\*