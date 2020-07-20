## IoT Population Health With Quarkus


### Architecture


### Running locally
The sections below provide the introductory commands to run the services for the Population Health PoC in a local development environment. Note that each service specifies a different port than the default since we'll be running more than one service in many scenarios.

**Prerequisites**
- maven 3.6.3+
- java 11+

#### Decision Services

The decision services platform can be run in a dev/local environment using the out of the box maven capability that ships with Quarkus.  Run:

`mvn clean compile quarkus:dev -Dquarkus.http.port=8081`

The service exposes an endpoint at `/healthRules` that will by default execute the Health Rewards and Health Alerts rule sets.

For example, to hit a rule in the Health Rewards ruleset:
```
curl -X POST "http://localhost:8081/healthRules" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"steps\":18000}"
```

See the [Data Format and Rules](#Data Format and Rules) section for more examples and details on the default rulesets.

#### Dashboard

#### Health Data ETL

### Deploy to AWS


### Future Functionality and Next Steps
