# ThreatMaaper
Open source cloud native security observability platform. Linux, K8s, AWS Fargate and more.

![deepfence-logo](https://user-images.githubusercontent.com/103250705/219148424-986efdf9-efc2-4e1d-a2fe-1d3c1ccf2600.png)


Announcing ThreatMapper 1.4

ThreatMapper 1.4.0 adds ThreatGraph, a rich visualization that uses runtime context such as network flows to prioritize threat scan results. ThreatGraph enables organizations to narrow down attack path alerts from thousands to a handful of the most meaningful (and threatening). Release 1.4.0 also adds agentless cloud security posture management (CSPM) of cloud assets and agent-based posture management of hosts, evaluating posture against industry-standard compliance benchmarks.

ThreatMapper - Runtime Threat Management and Attack Path Enumeration for Cloud Native

Deepfence ThreatMapper hunts for threats in your production platforms, and ranks these threats based on their risk-of-exploit. It uncovers vulnerable software components, exposed secrets and deviations from good security practice. ThreatMapper uses a combination of agent-based inspection and agent-less monitoring to provide the widest possible coverage to detect threats.

With ThreatMapper's ThreatGraph visualization, you can then identify the issues that present the greatest risk to the security of your applications, and prioritize these for planned protection or remediation.

![threatmapper-threatgraph-thumb](https://user-images.githubusercontent.com/103250705/219147475-3684d3f5-6cb7-4a5a-b689-d258290a0dab.jpg) ![threatmapper-vulnerabilities-thumb](https://user-images.githubusercontent.com/103250705/219148741-31481b54-1646-4bd9-9241-318983ca0257.jpg)

![threatmapper-topology-thumb](https://user-images.githubusercontent.com/103250705/219149133-982966e3-88bf-42fe-97f4-395c2fa00418.jpg)

When to use ThreatMapper

ThreatMapper carries on the good 'shift left' security practices that you already employ in your development pipelines. It continues to monitor running applications against emerging software vulnerabilities, and monitors the host and cloud configuration against industry-expert bnechmarks.

Use ThreatMapper to provide security observability for your production workloads and infrastructure, across cloud, kubernetes, serverless (Fargate) and on-prem platforms.

Getting Started with ThreatMapper

https://user-images.githubusercontent.com/103250705/219150606-e52cba70-8b69-4224-b3a2-6345ea15698e.mp4

Planning your Deployment

ThreatMapper consists of two components:

The ThreatMapper Management Console is a container-based application that can be deployed on a single docker host or in a Kubernetes cluster.
ThreatMapper monitors running infrastructure using agentless Cloud Scanner tasks and agent-based Sensor Agents

The Management Console

you deploy the managment console first, on a suitable docker host or kubernetes cluster. for Exmaple, On Docker 

# Docker installation process for ThreatMapper Management Console
sudo sysctl -w vm.max_map_count=262144 # see https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html

wget https://github.com/deepfence/ThreatMapper/raw/master/deployment-scripts/docker-compose.yml
docker-compose -f docker-compose.yml up --detach

Once the Management Console is up and running, you can register an admin account and obtain an API key.

Cloud Scanner tasks
ThreatMapper Cloud Scanner tasks are responsible for querying the cloud provider APIs to gather configuration and identify deviations from compliance benchmarks.

The task is deployed using a Terraform module. The ThreatMapper Management Console will present a basic configuration that may be deployed with Terraform, or you can refer to the expert configurations to fine-tune the deployment (AWS, Azure, GCP.

Sensor Agents
Install the sensor agents on your production or development platforms. The sensors report to the Management Console; they tell it what services they discover, provide telemetry and generate manifests of software dependencies.

The following production platforms are supported by ThreatMapper sensor agents:

Kubernetes: ThreatMapper sensors are deployed as a daemonset in the Kubernetes cluster, using a helm chart.
Docker: ThreatMapper sensors are deployed as a lightweight container.
Amazon ECS: ThreatMapper sensors are deployed as a daemon service using a task definition.
AWS Fargate: ThreatMapper sensors are deployed as a sidecar container, using a task definition.
Bare-Metal or Virtual Machines: ThreatMapper sensors are deployed within a lightweight Docker runtime.
For example, run the following command to start the ThreatMapper sensor on a Docker host:

docker run -dit --cpus=".2" --name=deepfence-agent --restart on-failure --pid=host --net=host --privileged=true \
  -v /sys/kernel/debug:/sys/kernel/debug:rw -v /var/log/fenced -v /var/run/docker.sock:/var/run/docker.sock -v /:/fenced/mnt/host/:ro \
  -e MGMT_CONSOLE_URL="---CONSOLE-IP---" -e MGMT_CONSOLE_PORT="443" -e DEEPFENCE_KEY="---DEEPFENCE-API-KEY---" -e USER_DEFINED_TAGS="" \
  deepfenceio/deepfence_agent_ce:1.4.2
  
  On a Kubernetes platform, the sensors are installed using helm chart

Next Steps
Visit the Deepfence ThreatMapper Documentation, to learn how to get started and how to use ThreatMapper.
