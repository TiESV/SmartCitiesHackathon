# Water Management Use Case

#

# Introduction

Africa has region that are faced with acute water problems. The provisioning of usable water to all households is a major concern in these regions.

The United Nations estimates that Sub-Saharan Africa alone loses 40 billion hours per year collecting water, that's the same as a whole year's worth of labor by France's entire workforce! This is incredibly valuable time.

With much of one's day already consumed by meeting basic needs, there isn't time for much else. The hours lost to gathering water are often the difference between time to do a trade and earn a living and not. Just think of all the things you would miss if you had to take three hours out each day to get water.

When a water solution is put into place, sustainable agriculture is possible. Children get back to school instead of collecting dirty water all day, or being sick from waterborne illnesses. Parents find more time to care for their families, expand minimal farming to sustainable levels, and even run small businesses.

The social and economic effects caused by a lack of clean water are often the highest priorities of African communities when they speak of their own development. The World Health Organization has shown this in economic terms: for every $1 invested in water and sanitation, there is an economic return of between $3 and $34!

This use case involves management of resources to provide water to maximum residents.

There could be a number of pitfalls both natural and manmade that could cause disruption in the water supply. To name a few issues, the water could get contaminated at a particular source, the source could run out of water, there could be act of vandalism leading to broken meters or pipes.

# Actors

- **Residents** : Inhabitants of the region. The residents need to acquire water everyday via one of the multiple means. One resident from each household is responsible for getting 125 liters of water per day (average household 2 adults with 3 kids. Per capital water is 25 liters per day).
- **Standpipes** : The standpipes are shared water pipe outlets in public locations to provide (sell) water to residents. They have fixed locations.
- **Wells:** Wells are alternative source of water to standpipes. If the NGO invests, they can be drilled in any location in the scope of the game.
- **Household Resellers:** Household resellers play a major role in the informal water market. These households have piped water connections, and decide to resell water to often neighbors who do not have pipe connections. Often they have a yard tap from which they provide and sell water.
- **Mobile Vendors:** Mobile vendors play the role of covering distant areas on the borders of the cities where other sources of water is far to reach. Buying from mobile vendors will avoid travel and wait time
- **NGO:** The NGO has a fixed amount of budget it can use to improve water access for residents. Each action it takes may incur costs, which deducts from the budget. It must give direction to each resident each day (via a mobile app), on which source they should go to get water on that particular day. The performance of the NGO is measured by the number of people it can guarantee water access on an average day during the course of the simulation

# Getting Started
To work with the TQL you will need to login into the **TQL Studio**.
Open the following URL in a browser of your choice: schack.tie.org:<port> (You will have to use the port provided to you)
Login credentials are, Username: <email id>, default password: <groupid>
On the home screen you see a tile for "IOT Simulated Apps". Clicking on this will take you to the Apps.
Click on the Water Management application to open it. 
On the Water Management screen, you will find a "Queries" tab. 
Clicking on the "Queries" tab will open the editor where you can create, edit and execute queries.
This Screen will also give you the URL to access application as a web service from external application.

# Queries to access the Models:

### Residents:

**Find all residents (****Using Find All****):**

```
{
"Query": {
        "Find": {
            "Residents": {
                "Id": {
                    "\_ne": ""
                }
            }
        }
    }
} 
```

**Find a resident by Name (****Using where condition****):**
```
{
    "Query": {
        "Find": {
            "Residents": {
                "Name": {
                    "\_eq": "Resident-1"
                }
            }
        }  	
	}	
}
```
**Count the number of residents (****Using count****):**

```
{
    "Query": {
        "Find": {
            "Residents": {
                "Id": {
                    "\_ne": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.Res.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```


**List of residents for a particular water source**
```
{
    "Query": {
        "Find": {
            "Residents": {
                "WaterSourceId": {
                    "eq": ""<!—Water source Id-->""
                }
            }
        }
    }
}
```

**Count of residents for a particular water source**

```
{
    "Query": {
        "Find": {
            "Residents": {
                "WaterSourceId": {
                    "\_eq": ""
                }
            }
        },
        "SetResponseData": {
            "key": "Message.Value.Res.Count",
            "value": "[:$Response.Message.Value.Find/count(Result):]"
        },
        "DelResponseData": {
            "key": "Message.Value.Find"
        }
    }
}
```

**Residents with water access:**

```
{
    "Query": {
        "Find": {
            "Residents": {
                "WaterAccess": {
                    "eq": "true"
                }
            }
        }
    }
}
```

**Residents without water access:**

```
{
    "Query": {
        "Find": {
            "Residents": {
                "WaterAccess": {
                    "\_eq": "false"
                }
            }
        }
    }
}
```

**Residents that got contaminated water:**

```
{
    "Query": {
        "Find": {
            "Residents": {
                "Contamination": {
                    "eq": "false"
                }
            }
        }
    }
}
```

**Residents with budget balance less that a particular value (Using less than)****:**

```
 {
     "Query": {
         "Find": {
             "Residents": {
                 "BudgetBalance": {
                     "lt": "3.4"
                 }
             }
         }
     }
 }
```

### Standpipes:

**Find all Standpipes:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find leaking standpipes:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "Leaking": {
                    "eq": "true"
                }
            }
        }
    }
}
```

**Find standpipes impaired for x days or more (Using greater than equal to)****:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "ImpairedDays": {
                    "ge": "2"
                }
            }
        }
    }
}
```

**Find standpipes impaired** **for more than x days (Using greater than)****:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "ImpairedDays": {
                    "gt": "2"
                }
            }
        }
    }
}
```

**Find standpipes with a particular tap condition broken or impaired (Using OR queries)****:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "or": {
                    "TapCondition": [
                        {
                            "eq": "broken"
                        },
                        {
                            "eq": "impaired"
                        }
                    ]
                }
            }
        }
    }
}
```

**Find Standpipes with contamination:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "Contamination": {
                    "eq": "false"
                }
            }
        }
    }
}
```

**Find Standpipes without attendants:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "Attendant": {
                    "eq": "false"
                }
            }
        }
    }
}
```

**Find Standpipes without attendant that are broken (Using and Queries)****:**

```
{
    "Query": {
        "Find": {
            "Standpipe": {
                "Attendant": {
                    "eq": "false"
                },
                "TapCondition": {
                    "eq": "broken"
                }
            }
        }
    }
}
```

### Well:

**Find all Wells:**

```
{
    "Query": {
        "Find": {
            "Well": {
                "Id": {
                    "ne": ""
                }
            }
        }
    }
}
```

**Find all metered Wells:**

```
{
     "Query": {
         "Find": {
             "Well": {
                 "MeterInstrumented": {
                     "eq": "true"
                 }
             }
         }
     }
}
```

### Mobile Vendor:

**Find all Mobile Vendors:**

```
{
     "Query": {
         "Find": {
             "MobileVendor": {
                 "Id": {
                     "ne": ""
                 }
             }
         }
     }
}
```

**Find Mobile Vendors that server in a Radius range (Using between)**

```
{
    "Query": {
        "Find": {
            "MobileVendor": {
                "Radius": [
                    {
                        "le": "0.6"
                    },
                    {
                        "ge": "0.5"
                    }
                ]
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

URL: [http://sandbox.atomiton.com:9099/fid-watermanagement](http://sandbox.atomiton.com:9099/fid-watermanagement)

Method: Post

Payload: The  desired query, e.g:

```
{
"Query": {
        "Find": {
            "Residents": {
                "Id": {
                    "\_ne": ""
                }
            }
        }
    }
} 
```

Result: Output of the Query

# Subscribing through a web-socket

URL: [ws://sandbox.atomiton.com:9099/fid-watermanagementws](ws://sandbox.atomiton.com:9099/fid-watermanagementws)

Using a websocket client, connect to the above URL.

The request will look like this:

```
{
    "Query": {
        "Find": {
            "Residents": {
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

TQL.Update.watermanagement.distribution.Standpipe.WaterSourceID.\*

TQL.Update.watermanagement.distribution.Standpipe.\*

TQL.Create.watermanagement.distribution.Standpipe.\*


Successful subscription results in an output like this:

```
<Query Storage="TqlSubscription">
    <Save>
        <TqlSubscription Label="MyLabel" sid="16">
		<Topic>\*</Topic>
        </TqlSubscription>
    </Save>
</Query>
```

```
<Save Status="Success">
  <TqlSubscription>
    <sid>TS3383311601768877182#016</sid>
    <Label Status="Success+Created:1:1447064746997;" Value="MyLabel"/>
    <Topic Status="Success+Created:1:1447064746998;" Value="\*"/>
  </TqlSubscription>
</Save>
```

This indicates a subscription is created and updated will now be sent over this socket.

The updates sent will look like this:

```
<TqlNotification>
  <Update>
		<KDWIJVXOAAAAUFAEGER4ZUM6>
			<watermanagement.distribution.Standpipe.WaterSourceID OldValue="" Value="" Version="54" Timestamp="1447077968713"/>
			<watermanagement.distribution.Standpipe.RecordDate OldValue="" Value="" Version="54" Timestamp="1447077968713"/>
			<watermanagement.distribution.Standpipe.QueueSize OldValue="" Value="" Version="54" Timestamp="1447077968713"/>
			<watermanagement.distribution.Standpipe.ImpairedDays OldValue="" Value="" Version="54" Timestamp="1447077968713"/>
			<watermanagement.distribution.Standpipe.EffectivePressure OldValue="" Value="" Version="54" Timestamp="1447077968713"/>
			<watermanagement.distribution.Standpipe.Leakage **OldValue="8.0000000000" Value="5.0"** Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.LeakIncrement OldValue="9.0000000000" Value="9.0" Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.FlowRate OldValue="" Value="" Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.PersonTime OldValue="" Value="" Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.WaitTime OldValue="" Value="" Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.MeterReading OldValue="" Value="" Version="54" Timestamp="1447077968714"/>
			<watermanagement.distribution.Standpipe.MeteredInstrument OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
			<watermanagement.distribution.Standpipe.WaterDemand OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
			<watermanagement.distribution.Standpipe.WaterSold OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
			<watermanagement.distribution.Standpipe.WaterRevenue OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
			<watermanagement.distribution.Standpipe.PressureSensor OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
			<watermanagement.distribution.Standpipe.AMR OldValue="" Value="" Version="54" Timestamp="1447077968715"/>
		</KDWIJVXOAAAAUFAEGER4ZUM6>
	</update>
</TqlNotification>
```

The watermanagement.distribution.Standpipe.Leakage is updated in this case.