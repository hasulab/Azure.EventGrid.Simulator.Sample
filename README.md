# Azure.EventGrid.Simulator.Sample
Azure EventGrid Simulator Sample

## Getting Started 

* Create a new ASP.NET Code empty Project
* Add latest [Hasulab.Azure.KeyVault.Simulator nuget library](https://www.nuget.org/packages/Hasulab.Azure.EventGrid.Simulator/) version
* Add following lines to Progarm.cs
```
builder.Services.AddLogging();
builder.Services.AddSimulatorServices(builder.Configuration);
//Other codes
app.MapSimulatorEndpoint();

```
* Add following sample Kestrel settings to appsettings.json or appsettings.Development.json

```
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "localhost-TestPASS1234.pfx",
        "Password": "TestPASS1234"
      }
    }
  },
  "EventDeliverySettings": {
    "CheckUpdateTime": 1000,
    "ConcurrentEventsProcessing": 2 
  }
```
and events subscriptions  settings to appsettings.json or appsettings.Development.json
```
"topics": [
    {
      "name": "MyLocalAzureFunctionTopic",
      "port": 5002,
      "key": "TheLocal+DevelopmentKey=",
      "subscribers": [
        {
          "name": "LocalAzureFunctionSubscription",
          "destination": {
            "endpointType": "WebHook",
            "properties": {
              "endpoint": "http://localhost:7071/runtime/webhooks/EventGrid?functionName=ExampleFunction",
              "disableValidation": true
            }
          },
          "filter": {
            "includedEventTypes": [ "TestEvent" ]
          }
        }
    }
  ]
```
* Press F5 or run the proejct
