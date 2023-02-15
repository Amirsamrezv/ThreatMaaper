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

"Once the Management Console is up and running, you can"
<a href="https://community.deepfence.io/docs/threatmapper/console/initial-configuration" rel="nofollow">register an admin account and obtain an API key</a>

# Cloud Scanner tasks

<p dir="auto">ThreatMapper <a href="https://community.deepfence.io/docs/threatmapper/cloudscanner/" rel="nofollow">Cloud Scanner tasks</a> are responsible for querying the cloud provider APIs to gather configuration and identify deviations from compliance benchmarks.</p>

<p dir="auto">The task is deployed using a Terraform module. The ThreatMapper Management Console will present a basic configuration that may be deployed with Terraform, or you can refer to the expert configurations to fine-tune the deployment (<a href="https://github.com/deepfence/terraform-aws-cloud-scanner">AWS</a>, <a href="https://github.com/deepfence/terraform-azure-cloud-scanner">Azure</a>, <a href="https://github.com/deepfence/terraform-gcp-cloud-scanner">GCP</a>.</p>

# Sensor Agents
<p dir="auto">Install the <a href="https://community.deepfence.io/docs/threatmapper/sensors/" rel="nofollow">sensor agents</a> on your production or development platforms. The sensors report to the Management Console; they tell it what services they discover, provide telemetry and generate manifests of software dependencies.</p>

The following production platforms are supported by ThreatMapper sensor agents:

<li><a href="https://community.deepfence.io/docs/threatmapper/sensors/kubernetes/" rel="nofollow">Kubernetes</a>: ThreatMapper sensors are deployed as a daemonset in the Kubernetes cluster, using a helm chart.</li>
<li><a href="https://community.deepfence.io/docs/threatmapper/sensors/docker/" rel="nofollow">Docker</a>: ThreatMapper sensors are deployed as a lightweight container.</li>
<li><a href="https://community.deepfence.io/docs/threatmapper/sensors/aws-ecs" rel="nofollow">Amazon ECS</a>: ThreatMapper sensors are deployed as a daemon service using a task definition.</li>
<li><a href="https://community.deepfence.io/docs/threatmapper/sensors/aws-fargate" rel="nofollow">AWS Fargate</a>: ThreatMapper sensors are deployed as a sidecar container, using a task definition.</li>
<li><a href="https://community.deepfence.io/docs/threatmapper/sensors/linux-host/" rel="nofollow">Bare-Metal or Virtual Machines</a>: ThreatMapper sensors are deployed within a lightweight Docker runtime.</li>

For example, run the following command to start the ThreatMapper sensor on a Docker host:

<pre>docker run -dit --cpus=<span class="pl-s"><span class="pl-pds">"</span>.2<span class="pl-pds">"</span></span> --name=deepfence-agent --restart on-failure --pid=host --net=host --privileged=true \
  -v /sys/kernel/debug:/sys/kernel/debug:rw -v /var/log/fenced -v /var/run/docker.sock:/var/run/docker.sock -v /:/fenced/mnt/host/:ro \
  -e MGMT_CONSOLE_URL=<span class="pl-s"><span class="pl-pds">"</span>---CONSOLE-IP---<span class="pl-pds">"</span></span> -e MGMT_CONSOLE_PORT=<span class="pl-s"><span class="pl-pds">"</span>443<span class="pl-pds">"</span></span> -e DEEPFENCE_KEY=<span class="pl-s"><span class="pl-pds">"</span>---DEEPFENCE-API-KEY---<span class="pl-pds">"</span></span> -e USER_DEFINED_TAGS=<span class="pl-s"><span class="pl-pds">"</span><span class="pl-pds">"</span></span> \
  deepfenceio/deepfence_agent_ce:1.4.2</pre>
  
  <p dir="auto">On a Kubernetes platform, the sensors are installed using <a href="https://community.deepfence.io/docs/threatmapper/sensors/kubernetes/" rel="nofollow">helm chart</a></p>
  
# Next Steps
<p dir="auto">Visit the <a href="https://community.deepfence.io/docs/threatmapper/" rel="nofollow">Deepfence ThreatMapper Documentation</a>, to learn how to get started and how to use ThreatMapper.</p>

# Get in touch
<p dir="auto">Thank you for using ThreatMapper.  Please feel welcome to participate in the <a href="/deepfence/ThreatMapper/blob/master/COMMUNITY.md">ThreatMapper Community</a>.</p>

<a href="https://community.deepfence.io" rel="nofollow">Deepfence Community Website</a>

 Got a question, need some help? Find the Deepfence team on Slack
Got a feature request or found a bug? Raise an issue
<a href="https://community.deepfence.io/docs/threatmapper/" rel="nofollow">Deepfence ThreatMapper Documentation</a>
<li><a href="/deepfence/ThreatMapper/blob/master/SECURITY.md">productsecurity at deepfence dot io</a>: Found a security issue?  Share it in confidence</li>
<li>Find out more at <a href="https://deepfence.io/" rel="nofollow">deepfence.io</a></li>

# Security and Support
<p dir="auto">For any security-related issues in the ThreatMapper project, contact <a href="/deepfence/ThreatMapper/blob/master/SECURITY.md">productsecurity <em>at</em> deepfence <em>dot</em> io</a>.</p>
Hub issues as needed, and join the Deepfence Community <a href="https://join.slack.com/t/deepfence-community/shared_invite/zt-podmzle9-5X~qYx8wMaLt9bGWwkSdgQ" rel="nofollow">Slack channel</a>.</p>

# License
<p dir="auto">The Deepfence ThreatMapper project (this repository) is offered under the <a href="https://www.apache.org/licenses/LICENSE-2.0" rel="nofollow">Apache2 license</a>.</p>
<p dir="auto"><a href="/deepfence/ThreatMapper/blob/master/CONTRIBUTING.md">Contributions</a> to Deepfence ThreatMapper project are similarly accepted under the Apache2 license, as per <a href="https://docs.github.com/en/github/site-policy/github-terms-of-service#6-contributions-under-repository-license">GitHub's inbound=outbound policy</a>.</p>
