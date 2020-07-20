## IoT Population Health With Quarkus

*  [Introduction](#Introduction)
*  [Architecture](#Architecture)
*  [Running locally](#Running locally)
    *  [Decision Services](#Decision Services)

### Introduction

This documentation provides an overview of the technical details and installation for the
IoT Population Health Quarkus implementation and submission for the the Quarkus Hackathon.

The objective of the architecture is to create an efficient, serverless, and rules driven architecture
that can be used to process health data telemetry from a wide array of devices and health data ecosystems.
By utilizing a rules driven approach the application gives enterprises the ability to customize data processing
via decision tables and in the future via business process management notation.    

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

For example, once up and running to hit a rule in the Health Rewards ruleset:
```
curl -X POST "http://localhost:8081/healthRules" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"steps\":18000}"
```

See the [Data Format and Rules](#Data Format and Rules) section for more examples and details on the default rulesets.

#### Dashboard

#### Health Data ETL

The implementation for the Health Data ETL service requires a connection to Google Fit APIs to fetch data. There are a number of steps required to authorize and connect Google APIs for execution in a local environment. If you want a simple experience to test decision services go to [Health Data Mock](#Health Data Mock)

The following steps all require a Google account and access to, or the ability to enable, a Google Cloud account.

**Setup a Client**
1. Visit cloud.google.com
2. Login and access the console
3. In the left nav select APIs & Services
4. Select Credentials
5. At the top select `+Create Credentials` button
6. Select OAuth client ID
7. In Application type select `Web application`
8. Enter a name for your app
9. Under `Authorized redirect URIs` enter the URL where you intend to run your health data service. If running locally enter `http://localhost:8080/oauth2callback`
    * If running deployed as a function in AWS then see the [Deploy to AWS](#Deploy to AWS) section below
10. **Hit Save**
11. Click on the row containing the client you just created in the steps above
12. Click `DOWNLOAD JSON` at the top of the screen
13. Save the file to a location of your choice (you'll need this path later)

**Configure the Application**
1. Open the application.properties file in `src/main/resources/application.properties`
2. Set the following required properties:
  * `google.fit.client.json.path` -- to the location of the `client_secret.json` file downloaded in the Setup a Client section above
  * `google.fit.api.token.store` -- an available folder location to store the refresh token for fit api calls


#### Health Data Mock

### Deploy Lambdas to AWS





### Future Functionality and Next Steps

- Refactor connectors to external services (like Google Fit) to quarkus extensions
- Dashboard UX
- Authentication and security on data services
