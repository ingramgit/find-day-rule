# Find day by date

Based on given date, The rule finds day for the date. If given date is 25-04-2024, The rule returns day as 'Thursday'.

Once you have deployed find-day_1.0.0 rule on Kie-server, then it can be accessed 
through below Kie-server REST API. We can test this API using below payload.

# URI: 
    http://<ip>/kie-server/services/rest/server/containers/instances/{MyContainer}
# Method: 
    POST
# Path Param: 
    You need to pass deployed container id in {MyContainer} placeholder
    Example: in our case deployed container id is find-day_1.0.0, so
    http://<IP>/kie-server/services/rest/server/containers/instances/find-day_1.0.0
# Headers: 
    Content-Type: application/json
    Authorization: Basic ************

# Request Payload:       
    {
        "commands": [
            {
                "insert": {
                    "object": {
                        "FindDay": {
                            "date": "25-04-2024"
                        }
                    },
                    "out-identifier": "deRequest",
                    "return-object": true
                }
            },
            {
                "fire-all-rules": {}
            }
        ],
        "lookup": null
    }

# Response Payload:
    {
        "type": "SUCCESS",
        "msg": "Container find-day_1.0.0-SNAPSHOT successfully called.",
        "result": {
            "execution-results": {
                "results": [
                    {
                        "value": {
                            "com.ingram.dataverse.FindDay": {
                                "date": "25-04-2024",
                                "day": "Thursday"
                            }
                        },
                        "key": "deRequest"
                    }
                ],
                "facts": [
                    {
                        "value": {
                            "org.drools.core.common.DefaultFactHandle": {
                                "external-form": "0:2:757684142:757684142:2:DEFAULT:NON_TRAIT:com.ingram.dataverse.FindDay"
                            }
                        },
                        "key": "deRequest"
                    }
                ]
            }
        }
    }