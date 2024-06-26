# FAQs 

## Manage FAQs

- **What are the benefits of moving to OpenShift?**

	<span style="color:navy">Some of the benefits are:</span>
	
	- <span style="color:navy">Portability between cloud/on-prem environments</span>
	- <span style="color:navy">Faster deployment compared to the traditional deployment model</span>
	- <span style="color:navy">More robust, resilient, high availability, and elasticity through containerization and container orchestration</span>
	- <span style="color:navy">Consistency per the operator model, repeatable deployment</span> 
	- <span style="color:navy">Capabilities for automating and streamlining the development process</span>
 
 
- **Do the operators need special configuration?**

	<span style="color:navy">
	Operators do not need any special configuration - their actions are driven by the CR (Custom Resource). Operators are the backbone of the automation in OpenShift/Kubernetes.  The operator's configuration is provided by the administrator via the MAS/Manage admin UI.  Behind the scenes, this UI updates the CR (which can also be manually changed). The operators run as pods in the OCP cluster.
	</span>


- **What is the purpose of the ingress controller?**

    <span style="color:navy">
	Ingress controller is OpenShift/Kubernetes way of exposing the service endpoint and load balancing to your applications.
	</span>

 
- **Can you elaborate on the IBM container registry (icr.io)?**
	
	<span style="color:navy">
	All IBM products’ images are stored there. The images are accessible if you purchased the product thus obtain an entitlement key. The entitlement key is to be provided when installing MAS, and the MAS and other application operators use this entitlement key to pull the images from icr.io.
	</span>
 
 
- **Are there options for organizations that are on windows or only options to provision new RHEL envs/move to cloud?**
	
	<span style="color:navy">
	Windows is not supported. The provided link is for setting up a development environment: <https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=administering-local-maximo-manage-development-environments>. You have the option to run it on bare metal or in VSphere. Additionally, for more information, refer to: <https://docs.openshift.com/container-platform/4.7/installing/index.html#supported-platforms-for-openshift-clusters_ocp-installation-overview>
	</span>

- **Are there any limitations to moving to OpenShift?**
	
	- <span style="color:navy">Potentially more hardware is needed for smaller installations.</span>
	- <span style="color:navy">Short term learning curve (like any new technology).</span>

- **Are there specific requirements for a multi-tenancy environment?**

	<span style="color:navy">
	Multi-Tenant Manage is not yet supported in MAS.
	</span>

- **Does OpenShift allow dynamic scaling?**

	<span style="color:navy">
	Yes, but MAS does not fully support it yet.
	</span>

- **Is the hypervisor something IBM provides or is that open source?**

	<span style="color:navy">
	There are different hypervisor products. IBM does not provide any hypervisor.
	</span>
  
- **What environment changes require application outages for users?**

	<span style="color:navy">
	Any change that requires the pods to go down. This is similar to today with when you need to restart the JVM.  For example, applying a new custom archive with your customization.
	</span>

- **What databases are supported?.**

	<span style="color:navy">
	All three databases (DB2,Oracle and SQL server) are supported for Manage.
	</span>

- **What Industry Solution/Add-ons are supported?**

	<span style="color:navy">
	All Industry Solutions/Add-ons are supported. Scheduler, Calibration, and Linear are now all included in base Manage. Life Sciences is covered via Calibration.
	</span>

- **What languages are supported?**

	<span style="color:navy">
	All 23 languages are supported.
	</span>

- **Are Oracle and SAP integrations supported?**
	
	<span style="color:navy">
	Yes, Oracle and SAP integrations are supported.
	</span>

- **What are the supported authentication methods in MAS?**

	<span style="color:navy">
	The following authentication methods are supported: 
	</span>
	
	- <span style="color:navy">Local IDP (username/password registered in Mongo DB)</span>
	- <span style="color:navy">LDAP </span>
	- <span style="color:navy">SAML </span>

	<span style="color:navy">Authentication Methods: </span><https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring-authentication-methods>


- **What authentication is needed for inbound HTTP/SOAP/REST-based integration to Manage?**

	<span style="color:navy">
	API Key authentication is required for inbound HTTP/SOAP-based integration to Manage. The API Key can be generated from the Manage administration app. The HTTP request header must include the API Key. For REST-based integration, you can use OIDC as well as an API key for authentication.
	</span>
    
	
- **What is the replacement of SI bus?**

	<span style="color:navy">
	Liberty JMS server, as well as Kafka community edition or any other supported JMS provider, are supported. Liberty JMS is available as a bundle from MAS config UI for any MAS Manage deployment.
	</span>

- **Is RMI supported?**

	<span style="color:navy">
	RMI is not supported outside of the Maximo server process. We recommend customers to leverage Maximo REST APIs instead of RMI. 
	
	RMI to Rest API: </span><https://ibm.box.com/s/5956jxr78i1bpihsvtrzub4wfb19p8o0>


- **Is BIRT reporting supported?**

	<span style="color:navy">Yes, BIRT is supported. Your reports will be moved automatically with the database upgrade.</span>


- **How does one restart the Manage server (other than deleting pods or restarting pods)?**

	<span style="color:navy">You can start and stop Manage server using the new tools-api.</span>
	
	- <span style="color:navy">Stop the Maximo Manage pods
		- POST </span> <https://host:port/toolsapi/toolservice/managestop>
	
	- <span style="color:navy">Start the Maximo Manage pods.
		- POST </span> <https://host:port/toolsapi/toolservice/managestart>
	
	<span style="color:navy">Start/stop and more administration APIs:</span>
		<https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=reference-apis-administrative-utilities>
		
- **Can we achieve the multiple JVMs functionality (in Maximo v7.x) for different Maximo Manage entities (UI, Cron, Reporting, MIF) and segregate the functionality accordingly?**
	
	<span style="color:navy">The Manage application can be deployed with different server bundles (workloads) for processing and isolation needs.</span>
    <span style="color:navy">The table below shows the different server bundles types: </span>
	
	|Bundle Server Type|Description|
	|------|-------|
	|all|This bundle type contains all the code.|
	|ui|This bundle type contains UI and supporting code. <br>It is the interface for accessing Manage application.|
	|mea|This bundle exposes the enterprise web services API.|
	|report|This bundle contains the code that is needed to enable <br> BIRT Report Only Server (BROS). Used to separate out <br>the work load that is related for execution of reports that <br> are submitted from the Manage UI.|
	|cron|This bundle contains the code that is needed to run <br> Manage cron tasks.|
	|standalonejms|This bundle is for Liberty Server JMS messaging, used by <br>Manage Integration Framework as the default JMS provider.|

- **How to deploy a custom Java class?**

	<span style="color:navy">
	The custom Java classes need to be packaged as a customization archive. A customization archive is a zip file and its structure is the same as the Maximo/SMP folder structure. It can include Java classes, XML, and database scripts. You need to follow the product.xml standard for customization. A customization archive is specified as part of the Manage CR spec (via the Manage deployment UI) so that the build process can include it. It can be accessed through the HTTP(s) or FTP(s) endpoint. Multiple customization archives are supported.
	</span>


- **How do we access the System.Out logs for Maximo?**

	<span style="color:navy">
	Manage server logs are written to the standard output. You can view the logs from the OpenShift console. </span>
	
	- <span style="color:navy">Go to your OpenShift console, navigate to the Workload/Pods menu, Select your Manage project.</span>
	- <span style="color:navy">Check your Liberty server pods. Select the server pod to view log. </span>
	
	<span style="color:navy">You can also use toolsapi to upload and retrieve logs using S3 storage.</span>
	

- **How can we run integrity checker?**

	<span style="color:navy">
	You can also use toolsapi to run integrity checker.
	</span>


- **How can we integrate Cognos with MAS?**

	<span style="color:navy">
	Cognos entitlement is included with MAS 8.10.
	</span>
	

- **How is LDAP configured in MAS?**

	<span style="color:navy">MAS uses WebSphere Liberty to synchronize with LDAP. Liberty provides a SCIM API for MAS to consume the data from LDAP repositories into the MAS user registry. MAS pushes users/groups to Manage from MAS repository using user sync process.</span>
	
	<span style="color:navy">LDAP configuration:</span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=identity-ldap-user-registry-synchronization>


- **How is the SMTP server configured?**

	<span style="color:navy">SMTP server is configured in MAS using the MAS Admin UI.</span>
	
	<span style="color:navy">SMTP configuration: </span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring-smtp-server>

- **How can certificates be applied?**

	<span style="color:navy">Cerificates can be applied via the MAS Admin UI.</span>
	
	<span style="color:navy">Certificate configuration: </span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=migrating-using-certificates>
	

- **What is the upgrade process?**

	<span style="color:navy">Upgrade Process: </span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=upgrading-from-maximo-asset-management-maximo-manage>

- **Are the Maximo users moved to MAS after upgrade?**

	<span style="color:navy">
	Yes, the Maximo users will have an entry created in MAS from the existing Maximo (7.6.1.2+) system during the upgrade execution.</span>
	
	<span style="color:navy">Migrated Users: </span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=migrating-managing-users-post-upgrade>


- **What are the EAM to Manage gaps?**

	<span style="color:navy">
	The following features/functionality are not supported yet, but are in the roadmap: 
	</span>

	<span style="color:navy;font-weight:bold">Functional gaps</span>
	- <span style="color:navy">E-Signature password should match with login password (LDAP/Local user)</span>
	- <span style="color:navy">Configuration of login page and common header</span> 
	- <span style="color:navy">User Self registration</span>
	- <span style="color:navy">Guest User</span>
	- <span style="color:navy">Allow LDAP synch mapping configuration</span>
	- <span style="color:navy">Ability to add unsupported language</span>
	- <span style="color:navy">Barcode font support</span>
	- <span style="color:navy">Archiving guidance</span>
	- <span style="color:navy">Configurable Email template for user management</span>
	- <span style="color:navy">Force user logout or similar</span>
	- <span style="color:navy">Ability to run custom metadata classes report</span>

	<span style="color:navy;font-weight:bold">Authentication</span>
	- <span style="color:navy">OpenID support in addition to SAML</span> 
	- <span style="color:navy">Support multiple LDAPs</span>
	- <span style="color:navy">Local user security controls parity</span>

	<span style="color:navy;font-weight:bold">Platform</span>
	- <span style="color:navy">Z Linux support</span>
	- <span style="color:navy">Power support</span>

	<span style="color:navy;font-weight:bold">Anywhere Migration</span>
	- <span style="color:navy">Calibration</span>
	- <span style="color:navy">Inventory - Transfer, Picking/Staging</span>

## Bug Fixes
- **How do I apply bug fixes?**

	- <span style="color:navy">Patches are periodically released with APAR fixes. It can be applied using the MAS Admin UI manually or automatically if you have subscribed.</span>
	
	- <span style="color:navy">LA(one-off) fixes can be applied using the customization archive process.</span>


- **What is the rollback process when a patch fails at the app layer or the db layer**

	<span style="color:navy">
	The rollback process include:
	</span>
	
	- <span style="color:navy"> Roll back the configuration, which is the Manage Workspace CR and its associated secrets in the OpenShift Manage namespace.  The old image can be regenerated by the operator, or the old build can be specified to have the deployment revert back toa previous state.</span>
	
	- <span style="color:navy"> Restore the database. (Same as 7.6) </span>
	
	<span style="color:navy"> A new back-up and restore instruction document will be delivered in Manage 8.4. </span>


## Useful Links

<span style="color:navy">
Upgrading from IBM Maximo Enterprise Asset Management to IBM Maximo Manage:</span>
<https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-integration#concept_ecy_3dv_5tb>

<span style="color:navy">Maximo Application Suite:</span>
<https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring>


## Terminology

|Term|Description|Used For|
|------|-----|-----|
 Admission Webhook|Admission webhooks are HTTP callbacks that receive admission requests <br> and do something with them.|We are using them to control the product matrix as part of the <br> deployment process(eg cannot install both HSE and Oil & Gas).|
|Ansible|Ansible is an open-source software provisioning, configuration management, <br> and application-deployment tool enabling infrastructure as code.|<br>Used for deploying pods 
|ConfigMap|Config maps hold configuration data for pods to consume. This is <br> similar to a property file.|Internally generated from CR|	
|CR<br>(Custom Resource)|A resource implemented through the Kubernetes Custom Resource <br> Definition  API. A resource is an endpoint in the Kubernetes API that stores <br> a collection of API objects of a certain kind; for example, the built-in pod's <br>resource contains a collection of Pod objects. A custom resource is distinct <br>from the built-in Kubernetes resources, such as the pod and service <br>resources. Every CR is part of an API group.|Manage CRs: <br>  * ManageApp <br>  * ManageWorkspace <br>  * ManageBuild <br>  * ManageDeployment <br>  * ManageAppStatus<br> * ManageServerBundles <br> <br>  * BuildDataInterpreter (for ACM)|
|CRD <br>(Custom Resource Definition)| Create a custom resource definition to define a new custom resource. CRD <br> is to CR as XSD is to XML. <br>|Manage CRs: <br> * ManageApp <br> * ManageWorkspace <br> * ManageBuild <br> * ManageDeployment <br> * ManageAppStatus<br><br> * ManageServerBundles <br> <br>* BuildDataInterpreter (for ACM)|
|EFK (Elastic search, FluentD,<br>Kibana)|The EFK stack is a modified version of the ELK stack and is comprised of:<br> * Elasticsearch: An object store where all logs are stored.<br>  * Fluentd: Gathers logs from nodes and feeds them to Elasticsearch. <br> * Kibana: A web UI for Elasticsearch. <br><br> Once deployed in a cluster, the stack aggregates logs from all nodes and <br>projects into Elasticsearch, and provides a Kibana UI to view any logs. <br> <br>Cluster administrators can view all logs, but application developers can <br> only view logs for projects they have permission to view. The stack <br>components communicate securely.| Used for Log Analysis |
|Entitled Registry|Where IBM stores the images for download and use in MAS|This is where we keep binaries that will be used to build an image.|
|Image|An image is a binary that includes all of the requirements for running a <br>single container, as well as metadata describing its needs and capabilities.|This is what is deployed as Manage, Monitor, Assist, etc.|
|Kafka|Apache Kafka is a framework implementation of a software bus using <br>stream-processing.|It is a pre-req for Monitor.  For Manage, it is an option that <br>can be used as a JMS queue alternative.|
|Kubernetes aka K8s|Kubernetes is a portable, extensible, open-source platform for managing <br> containerized workloads and services.|Maintains the "cluster"|
|MAS<br>(Maximo Application Suite)|The main entry point for working with the Maximo applications <br>(Manage, Assist, etc)||
|Manage|Formerly Maximo EAM||
|MongoDB|A NoSQL database - a document database, which means it stores data in <br>JSON-like documents.|MAS user and license metric information is stored here|
|Namespace/Project|Kubernetes provides a partitioning of the resources it manages into <br>non-overlapping <br> sets called namespaces|In MAS, there is a namespace for Manage, a namespace for Assist, etc. <br> In the future, there can be multiple instances of an application(eg Manage)<br> per namespace.|
|OCP<br>(OpenShift Container Platform)|An on-premises platform as a service built around Docker containers <br>orchestrated and managed by Kubernetes|Manages the MAS cluster|
|OIDC<br>(Open ID Connect)|A simple identity layer on top of the OAuth 2.0 protocol|Used for authentication between MAS and Manage|
|OIDP<br>(Open ID Provider)|An identity provider, or OpenID provider (OP) is a service that specializes <br>in registering OpenID URLs or XRIs.|Used for authentication between MAS and Manage|
|Operator|Operators are software extensions to Kubernetes that make use of custom <br>resources to manage applications and their components.|Processing within MAS|
|Persistent Volume|A PersistentVolume (PV) is similar to drive mapping. This API object <br>captures the details of the implementation of the storage, be that NFS, <br>iSCSI, or a cloud-provider-specific storage system.|In Manage we use PV to map with attached docs or other places where similar access <br>is needed.|
|Pods|Pods are the smallest, most basic deployable objects in Kubernetes. A <br>pod represents a single instance of a running process in your cluster. <br>Pods contain one or more containers, such as Docker containers. When <br>a pod runs multiple containers, the containers are managed as a single <br>entity and share the Pod's resources.|Deploying a Maximo "server"|
|RHEL<br>(RedHat Enterprise Linux)|Red Hat Enterprise Linux (RHEL) is a Linux-based operating system <br>from Red Hat designed for businesses. RHEL can work on desktops, <br>on servers, in hypervisors or in the cloud. Red Hat and its community-<br>supported counterpart, Fedora,is among the most widely used Linux <br> distributions in the world.||
|RHCOS<br>(RedHat Core Operating System)|The version of RHEL that comes as part of OCP|If you are installing on<br> bare metal, then this is the operating system being used|
|Route|An OpenShift route is a way to expose a service by giving it an externally-<br>reachable hostname like www.example.com. A defined route and the <br> endpoints identified by its service can be consumed by a router to provide <br>named connectivity that allows external clients to reach your applications.|Replacement of IHS in EAM.  The route plus the service is used for external access.|
|SCIM<br>(System for Cross-domain Identity <br>Management)|A set of standardized HTTP endpoints for searching, updating, and deleting <br> user records using JSON formatted data. It also includes standards and <br>guidelines to define how user data should be formatted and sent from an <br>Identity provider to an application (and vice-versa)|Internally used for <br>LDAP processing between MAS and Manage via WAS Liberty|
|Scratch Image|A non-runnable image that is used to build the final image.|Each Industry Solution, Add-On and Customization package is a scratch image that is <br>combined with the base Manage image to create the finally deployed image in MAS|
|Service Bindings|A way to create a Kubernetes-wide specification for communicating <br>service secrets to applications in an automated way.||
|Service Bundle/workload|Part of the CR/CRD definition in regards to the various Manage server types|Denotes type and number of Manage pods - UI, Cron, MEA, Report, All, etc|
|SLS<br>(Suite License Server)|This is the server that process AppPoints|AppPoints|
|UBI<br>(Universal Base Image)|A vehicle for building and delivering certified containers and operators|Used as a base for creating the Manage image(s). <br>Manage uses the RedHat UBI and Liberty UBI.|
|Watches|An operator subscription to the create/change/delete event of certain OCP <br>resources. These are specifid in watches.yaml and used internally only.|Allows for processing new selections of deployment (for example, add a language)|
|Workspace|An aggregation of namespaces used to create a MAS sub-instance. In 8.5 <br> and earlier there is always only one workspace.  In the future, within MAS <br>one could define different workspaces.|Similar to Namespace, but this is for MAS as a whole. Each workspace could have <br>a different configuration. This would be useful for sharing a MAS instance between <br>dev and QA environments.|
|YAML<br>(YAML Aint Markup Language)|YAML is a human-readable data-serialization language. It is commonly <br>used for configuration files and in applications where data is being <br> stored or transmitted.|Used to define CRDs/CRs|

