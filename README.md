![deepfence-logo](https://user-images.githubusercontent.com/103250705/219159739-728f5831-8574-44ba-8fde-9f586f603ca2.png)

# 🎉 Announcing ThreatMapper 1.4
 adds ThreatGraph, a rich visualization that uses runtime context such as network flows to prioritize threat scan results.  ThreatGraph enables organizations to narrow down attack path alerts from thousands to a handful of the most meaningful (and threatening). Release 1.4.0 also adds agentless cloud security posture management (CSPM) of cloud assets and agent-based posture management of hosts, evaluating posture against industry-standard compliance benchmarks.
 
# ThreatMapper - Runtime Threat Management and Attack Path Enumeration for Cloud Native
Deepfence ThreatMapper hunts for threats in your production platforms, and ranks these threats based on their risk-of-exploit. It uncovers vulnerable software components, exposed secrets and deviations from good security practice. ThreatMapper uses a combination of agent-based inspection and agent-less monitoring to provide the widest possible coverage to detect threats.

With ThreatMapper's ThreatGraph visualization, you can then identify the issues that present the greatest risk to the security of your applications, and prioritize these for planned protection or remediation.

![threatmapper-topology-thumb](https://user-images.githubusercontent.com/103250705/219166809-8e927633-3255-4ade-a05c-85206ac801a3.jpg)
                                                 
                                                 Learn the Topology	
                                                 
![threatmapper-vulnerabilities-thumb](https://user-images.githubusercontent.com/103250705/219167228-016423a8-f4ca-4752-9664-959cffc83fad.jpg)

                                                  Identify Threats	
                                                  
![threatmapper-threatgraph-thumb](https://user-images.githubusercontent.com/103250705/219168366-fcbcb7fe-03ff-46dc-abcc-993581ed8002.jpg)

                                                   Explore the ThreatGraph


<a href="https://community.deepfence.io/docs/threatmapper/" rel="nofollow">Learn more about ThreatMapper</a>
<a href="https://community.deepfence.io/docs/threatmapper/demo" rel="nofollow">See ThreatMapper running</a>


# When to use ThreatMapper

ThreatMapper carries on the good 'shift left' security practices that you already employ in your development pipelines. It continues to monitor running applications against emerging software vulnerabilities, and monitors the host and cloud configuration against industry-expert bnechmarks.

Use ThreatMapper to provide security observability for your production workloads and infrastructure, across cloud, kubernetes, serverless (Fargate) and on-prem platforms.

# Getting Started with ThreatMapper
https://user-images.githubusercontent.com/103250705/219170188-b2e77c19-5396-4176-8601-cfa0d5a0f1c0.mp4

# Planning your Deployment
ThreatMapper consists of two components:

The ThreatMapper Management Console is a container-based application that can be deployed on a single docker host or in a Kubernetes cluster.
ThreatMapper monitors running infrastructure using agentless Cloud Scanner tasks and agent-based Sensor Agents

<h3>The Management Console</h3>

<a href="https://community.deepfence.io/docs/threatmapper/console/" rel="nofollow">deploy the Management Console first</a>

<pre><span class="pl-c"><span class="pl-c">#</span> Docker installation process for ThreatMapper Management Console</span>
sudo sysctl -w vm.max_map_count=262144 <span class="pl-c"><span class="pl-c">#</span> see https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html</span>

wget https://github.com/deepfence/ThreatMapper/raw/master/deployment-scripts/docker-compose.yml
docker-compose -f docker-compose.yml up --detach</pre>
