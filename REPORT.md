# Report

## Solution
1. k8s manifests were created. As the very first step they were created by kompose util, so that is why the labels are still there.
Additionally I had to change fortuneSlice.ts in frontend/src/features/fortune. The solution is ugly I put in line #17 following:
('http://backend.default.svc.cluster.local:8080/');
 instead of http://localhost:8080. 
 Not to have uggly solution a variable would need to be setup here and it should be deifned on deployment/pod  level of frontend,     
2. To show you what I was doing during the debug you can see commented out lines in backend manifets, where I tried to put both containers in one pod to check their communication. This would not definitely be a good solution, but to show you what I was doing.
3.  Attaching screenshots & frontend log regarding deployment.
![alt text](k8s/images/browser.odg "Browser")
![alt text](k8s/images/logs.odg "Logs")

### Questions
1. **CI/CD**
   - How would you set up a basic CI/CD pipeline to build, test, and deploy the microservices to the remote Kubernetes cluster?

   Clone source code, build docker images, push image to registry, inspect the image for vulnerabilities, execute local automatic tests or deploy to test env and excute tests there. In case tests passed pormote to next env. Deployment type to PROD whether manual or automatic depends on plenty of circumstances so  I would leave it as open for now.

   - What deployment strategy would you recommend for deploying updates to the microservices in the Kubernetes cluster, and how would you implement it in the CI/CD pipeline?

   Most common is rolling Update. Additionally I would consdier Blue Green and/or Canary. This is a part of yaml manifests setup.

2. **Metrics**:
   - What tools or platforms do you use for collecting and visualizing metrics in a Kubernetes environment?
   
   Grafana or DataDog.

   - What are some key metrics you would monitor for a Kubernetes cluster and why?

    Cluster CPU, memory usage
    Number of nodes in the cluster
    Number of pods in the cluster
    Number of containers running in the cluster
    Network throughput and latency
    Disk usage and I/O operations
    Responses latency 
    Errors inresponses.
   
   Some of them are typical technical, but some of them are user experience related. Having them we can look for relation and find a bottleneck in resources.




3. **Logging**:
   - Describe your approach to centralized logging in a Kubernetes environment.

   Use common tools. hopwever in general it turns out that not the tools provided by cloud provider.

   - What tools do you prefer for log aggregation and analysis, and why?
   
   DataDog. Very intuitive tool and easy to get what you are looking for. On the other hand expensive.

4. **Monitoring**:
   - What is your process for setting up monitoring alerts in Kubernetes?

   Either experience would suggest what to monitor, if no experience then excute load tests and upon analysis the decide whatt to monitor.

   - How do you ensure high availability and fault tolerance in your monitoring setup?

   Well, I would say that exactly same guidlines as for other systems do apply here. 
