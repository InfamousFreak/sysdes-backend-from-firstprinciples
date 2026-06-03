**TELEMETRY BACKEND : **
centralized server, db or cloud plat that receives, processes stores and visualizes system performance data sent from applications. 

when app generate health data, they dont look at it, they ship that raw data into telemetry backend, which is this brain for monitoring our software's health 

**Ingests 3 pillars of observability : **
metrics : quantitative data showing system vitals
logs : text records of specific events that occured at a timestamp
traces : map tracking a single user request as it ttavels across multipel serves, dbs and microservices, showing exactly where lag errors occured. 


**Architecture : how data gets to backend :- **

modern systems use standardized tools like **opentelemetry **to separate code compilation from storage layer


app code -> otel collector -> otlp protocol -> telemtry backend

client app : generates the raw log, metric or trace
collector : acts as middleman to aggregate, clean and compress the incoming stream
backend : receives the clean stream, saves it to specialzed db, populates interactive dbs


**Why need separate backend ? **

- massive scale : telemetry generates millions of data points every minute, standard app dbs liek mysql cannot handle that write volume w/o slowing down user facing app
- specialized dbs : telemetry backends use time-series dbs optimzed for quickly queryying timestamps, ranges and trends
- alerting engines : continuous bg loops to scan incoming telemetry and instantly trigger slack or pagerduty alters if error spikes are found


Metrics : prometheus (open), datadog - amazon cloudwatch (managed)
Traces : jaeger grafana tempo (open), honeycomb(managed)
logs : grafana loki, opensearch(open), loggly, sumo logic (commercial)

**Auto recovery configuration : **

set of rules we define that tells our paas, how to automatically detect destroy and restart containerized application if it crashes, freezes or becomes unresponsive

- ensures application remains highly available to users 24/7, without a huma to manually do health checks and restarts if anything wrong 

**HOW DOES IT WORK?**

Has 3 mechanisms to manage auto recovery : 

1. paas continously monitors your container to ensure it is healthy, configure specific 2 tests : 
              - liveness probes : platform periodically pings a specific url endpoint in my app (/*healthz)*, or checks if the container is running, if app returns error or fails to respond, paas marks it as dead
                - readiness probes : checks if app is finished booting and ready to accept user traffic, if fails, paas stops sending users to that container but won't kill it yet


2. Restart Policies : once a failure is detected, the paas executes your predefined restart policy. In a containerised envs, these are usual variations of docker's native restart instructions : 
    
      - *on - failure* : restarts the container only if the application exits with an error code 
      - *always : *restarts the container regardless of why it stopped (even if it ws a clean exit)
      - *unless-stopped : *restarts the container continuously unless a developer explicityly turns it off

3. Rolling updates and circuit breakers (protection) 

 if a broken version of code is deployed that crashes instalty upon starting, a good paas auto recovery system will protect your users. It keeps your old working container alive while attempting to boot a new one. If the new container fails its health check, paas rolls back the deployment and soudns an alarm, keeping your website online. 