
IDP is built on an extensible microservices architecture. It leverages the orchestration capabilities of the widely popular Jenkins and provides a layer of abstraction over it through Angular 5 based responsive web front end and Spring Boot based RESTful services.

**IDP satisfies the 15 factors [guidelines from PIVOTAL](https://content.pivotal.io/blog/beyond-the-twelve-factor-app), for a highly scalable and resilient Cloud App.**

Below diagram depicts the high level architecture of IDP.

![](https://github.com/Infosys/openIDP/blob/master/docs/architecture_images/idp_architecture.png)

The table below explains the key components of IDP.

<table>
<colgroup>
<col width="150" />
<col width="800" />
</colgroup>

<tbody>
<tr>
  <th align="center">Module/File</th>
  <th align="center">Description</th>
</tr>
<tr>
  <td align="center"><b>UI</b></td>
  <td>This component is built on Angular 6 and TypeScript and supports seamless rendering in Mobile devices and tablets. All external API calls are routed through Zuul Filter from Netflix. Through Pre/Route/Post, Zuul will make sure only authenticated users are allowed to make API calls and for OAuth2 token renewal


  </td>
</tr>
<tr>
  <td align="center"><b>Cloud Config Service</b></td>
  <td>This component maintains all the config entries of IDP Components. This way, all configurations are externalized. Config files can be configured per environment and per client which gives greater flexibility 
When a service is booting up, it fetches the appropriate config files from this Service
  </td>
  
</tr>
<tr>
  <td align="center"><b>Discovery Service</b></td>
  <td>Eureka from Netflix is used. Services get registered following Self-Registration Pattern. The service registry provides a management API and a query API for registering/de-registering.
  </td>
  
</tr>

<tr>
  <td align="center"><b>Auth Service</b></td>
  <td>Auth Service's purpose is to authenticate users and manage OAuth2 tokens. Access token is generally short lived and refresh token would be valid for a long time. This supports Token Renewal and protects from MITM attacks. JSON Web Token(JWT) ensures the user’s session is handled in a stateless scalable way
  </td>
  
</tr>

<tr>
  <td align="center"><b>IDP Rest</b></td>
  <td>This service responsible for Application, Pipeline, User and Dashboard Management. It uses Swagger for API Documentation. Resources are protected using OAuth2 API First approach and Entities are defined using Google’s GSON. Uses Spring-boot for automating and simplifying and bootstrapping  boiler plate.
  </td>
  
</tr>

<tr>
  <td align="center"><b>DSL</b></td>
  <td>DSLs are the core for automating the Jenkins Job Creation. This is a hybrid approach for creating Jenkins jobs using Groovy. Seed Job gets created through REST service and this job in turn creates the child Jobs (SCM, Build, Deploy etc) . When the Seed Job is re-run, DSL is intelligent enough to identify the differences in configuration and would automatically create/update/delete job/configurations
  </td>
  
</tr>

<tr>
  <td align="center"><b>Scheduler</b></td>
  <td>This Java based component is for timed execution of pipelines.
  </td>
  
</tr>

<tr>
  <td align="center"><b>Metrics Dashboard</b></td>
  <td>Grafana is used for visualising the data collected by dashboard utilities (Java utilities that are invoked at the end of every job in the pipeline) through the dashboard "put" services. The "get" type of dashboard services query this data and offer it to Grafana for rendering and visualisation. 
  </td>
  
</tr>

<tr>
  <td align="center"><b>Message Queue</b></td>
  <td>Apache Kafka is used for asynchronous communication between services
  </td>
  
</tr>

<tr>
  <td align="center"><b>Continuous deployment</b></td>
  <td>This components provides seamless ability to do cloud deployments. This is not yet part of the repository and will soon be released.
  </td>
  
</tr>

<tr>
  <td align="center"><b>Subscription</b></td>
  <td>This component maintains the license information for the platform and to enable subscription based access. This is not yet part of the repository and will soon be released.
  </td>
  
</tr>
<tr>
  <td align="center"><b>Tracing</b></td>
  <td>Tracing of REST Service calls is done using ZipKin, a distributed tracing system. This gathers timing data that is required to troubleshoot latency. This component matches, both the collection and lookup of this data. This is not yet part of the repository and will soon be released.
  </td>
  
</tr>

<tr>
  <td align="center"><b>Monitoring</b></td>
  <td>IDP components' monitoring is done using Prometheus. The Prometheus agent extracts logs and pushes to Elastic Search from which data is data is propagated to Grafana. This is not yet part of the repository and will soon be released.
  </td>
  
</tr>