# Required configuration

AKM .NET library requires specific configuration items present in application's
configuration file (like appsettings.json)

```JSON
"AkmAppConfigs": [
  {
    "SelfAddressValue": 1,
    "DefaultKeySize": 32,
    "NumberOfKeys": 4,
    "RelationshipId": 1,
    "FrameSchema": {
      "RelationshipId_Index": 0,
      "RelationshipId_Length": 2,
      "SourceAddress_Index": 2,
      "SourceAddress_Length": 2,
      "TargetAddress_Index": 4,
      "TargetAddress_Length": 2,
      "AkmEvent_Index": 6,
      "AkmEvent_Length": 1,
      "AkmDataStart_Index": 7
    },
    "InitialKeys": [
      {
        "InitialKey": "6v9y$B&E)H+MbQeThWmZq4t7w!z%C*F-"
      },
      {
        "InitialKey": "z$C&F)H@McQfTjWnZr4u7x!A%D*G-KaN"
      },
      {
        "InitialKey": "6v9y$B&E)H+MbQeMhWmZq4t7w!z%C*Fo"
      },
      {
        "InitialKey": "z$C&F)H@McQfTjWaZr4u7x!A%D*G-Kat"
      }
    ],
    "NodesAddresses": [ 1, 5 ]
  }
]
```

This information is used to configure AKM library and state machine for specific
Relationship group based on Relationship ID value.
