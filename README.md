### Background
Security is a highly dynamic topic with ever changing threats and priorities. Newsworthy topics ranging from fortune 500 companies like [Garmin](https://www.wired.com/story/garmin-ransomware-hack-warning) paying $10 million in ransom for ransomware attacks to supply chain attacks such as [Lapsus$](https://www.theverge.com/2022/4/20/23034360/okta-lapsus-hack-investigation-breach-25-minutes) are ever-present. 

Security is becoming harder for engienering teams as the velocity of service deployments is accelerating. The [Synopsis 2022 Open Source Security Risk Analysis Report](https://www.synopsys.com/content/dam/synopsys/sig-assets/reports/rep-ossra-2022.pdf) revealed that 78% of audited code bases was open source, and within those codebases, 81% contained at least one vulnerabiltiy, which creates risk if left unpatched. With "shifting right", the industry has doubled down on incorporating security validations into each step of the build -> from the local dev environemnt -> to linters commit and pull request review -> to ci/cd checks during the deployment process, incorporating check into nominal deployment process are vital to identify security defects before they hit production.

Your company CTO is worried about what your engineering team is doing to harden and monitor the company's new microservices against malicious threat actors and payloads. You’ve completed the exercies in the course and have a baseline understanding of how to approach this. In response to the CTOs concerns, students will threat model and build a hardened  microservices stack based on what they learned from the exercises.

### Goal 
You will be presented with the challenge to build a secure microservice stack, threat modeling and hardening the container image, run-time environment and application itself. For purposes of the project, you will be instructed to use a secure base opensuse image, covering considerations for the importance of using trustworthy base images and verifing the baselein. You will be provided with instructions to build, harden, ship and run an environment analogous to the company's new microservice, simplified for project purposes. In the project you will define and build a new environment from the ground-up. 

In a real-world scenario, you may have an existing envrionment that needs to be hardened or it may decided to re-build parts or all net-new, regardless, the tools and techniques in the project are directly applicable. The beauty of microservices vs a monolith architecture is that all core components (image, container, run-time, application) are abstracted allowing for isolation boundaries and iterative development. In the real-world, you could chose to harden and redeploy all base-images as one project phase and tackle docker container security, kubernetes hardening and the software composition anaylsis, as individual project phases. 

The best approach is to incorporate these requirements and security hardening into the build and deploy processes. In an enterprise setting, much of this can be enforced with linters on commit and PR review and security units test via CI/CD prior to deployment. Hardening the base-image and incorporating security checks into the CI/CD is beyond the scope of this project and course, however please reference the [additional considerations](https://github.com/udacity/nd064-c3-Microservices-Security-project-starter/tree/master/starter#additional-considerations) section for more on this. 

For the project, once the microservice stack is hardened and provisioned, we will configure [sysdig Falco](https://github.com/falcosecurity/falco) to perform run-time monitoring on the node, sending logs to a Grafana node for visualization. To demonstrate to the CTO that the company can respond to a real security event, you will then simulate a [tabletop cyber exercise](https://www.tripwire.com/state-of-security/security-data-protection/everything-you-need-to-know-about-cyber-crisis-tabletop-exercises/) by running a script to introduce an unknown binary from the starter code that will intentionally disrupt the environment.  

No stress, you have tools, security engineering and security incident response knowledge to respond :) Your goal will be to use Falco events visualized in Grafana to determine what the unknown binary is, contain and remediate the environment, write a post-mortem incident response report and present it to the CTO. There will be a few hidden easter eggs, see if you can find them for extra credit! 

### Project Instructions

Follow the steps/instructions in the Udacity classroom to complete and submit the project.



kubectl apply   --validate=false -f https://github.com/cert-manager/cert-manager/releases/download/v1.3.1/cert-manager.yaml  
helm install  cert-manager jetstack/cert-manager  --namespace cert-manager --create-namespace --version v1.3.1
helm install  falco-exporter --namespace falco --set serviceMonitor.enabled=true falcosecurity/falco-exporter

helm list  --all --all-namespaces


prometheus
helm list --all --all-namespaces


kubectl  edit prometheus kube-prometheus-stack-1670-prometheus -n monitoring

kubectl  apply -f falco_service_monitor.yaml
