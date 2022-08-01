# Manage FAQs (MAS 8.8/Manage 8.5)

## Manage
- ** What's new?**

	
	- <span style="color:navy">**OpenShift Operators:** The installation, configuration, deployment, the upgrade is performed by the OpenShift operator.</span>
	- <span style="color:navy">**Security & User Management:** The authentication and user management is configured in MAS. All users will be synchronized into Manage from MAS. All headless interactions (Integration, REST) require API Key for authentication.</span>	
	- <span style="color:navy">**Application Server:** WebSphere Liberty will be used as a runtime to run the code in a containerized environment in Red Hat OpenShift. WebSphere ND and WebLogic are not supported.</span>	
	- <span style="color:navy">**Integration:** RMI is replaced by REST API.</span>	
	- <span style="color:navy">**Message Queue:** If you are using SI Bus, you can use Liberty JMS server, Kafka or any other supported JMS provider.
    </span>

- **Do the operators need a special configuration?**

	<span style="color:navy">
	Operators do not need any special configuration - their actions are driven by the CR (Custom Resource). Operators are the backbone of the automation in OpenShift/Kubernetes.  The operators’ configuration is provided by the administrator via the MAS/Manage admin UI.  Behind the scenes, this UI updates the CR (which can also be manually changed). The operators run as pods in the OCP cluster.
	</span>

- **What is the use of the ingress controller?**

    <span style="color:navy">
	Ingress controller is OpenShift/Kubernetes means of exposing the service endpoint and load balancing to your applications.
	</span>

- **What are the benefits of moving to OpenShift? More robust, quicker time to deliver infrastructure, do you already have a list?**

	<span style="color:navy">There are a number of items:</span>
	
	- <span style="color:navy">Portability between cloud/on-prem environments</span>
	- <span style="color:navy">Faster deployment compared to the traditional deployment model</span>
	- <span style="color:navy">More robust, resilient, HA, and elasticity through containerization and container orchestration</span>
	- <span style="color:navy">Consistency through the operator model, repeatable deployment</span> 
	- <span style="color:navy">Capabilities for automating and streamlining the development process</span>
 
 
- **Can you please elaborate on ibm icr.io?**
	
	<span style="color:navy">
	It is IBM’s container registry. All IBM products’ images are stored there. The images are accessible if you purchased the product thus obtain an entitlement key. The entitlement key is to be provided when installing MAS, and the MAS and other application operators use this entitlement key to pull the images from icr.io.
	</span>
 
 
- **For organizations that are on windows, are there options or only options to provision new RHEL envs /  move to cloud?**
	
	<span style="color:navy">
	You can run on bare metal or in VSphere.  See also: <https://docs.openshift.com/container-platform/4.7/installing/index.html#supported-platforms-for-openshift-clusters_ocp-installation-overview>
	</span>

- **What is the one big limitation of moving to OpenShift?**

	<span style="color:navy">
	- Potentially more hardware is needed for smaller installations.
	- Short term learning curve (like any new technology.
    </span>

- **Are there specific requirements for a multi-tenancy environment?**

	<span style="color:navy">
	MT is not yet supported in OpenShift.
	</span>

- **Does OpenShift allow dynamic scaling?**

	<span style="color:navy">
	Yes, but MAS is not fully there yet.
	</span>

- **Is the hypervisor something IBM provides or is that open source?**

	<span style="color:navy">
	There are different hypervisor products. Windows server datacenter solution provides windows hypervisor license.
	</span>

- **Where does that plan into the diagram if you were to use windows?**

	<span style="color:navy">
	Windows is not supported at this time unless using vSphere.  
	</span>
  
- **What environment changes require application outages for users?**

	<span style="color:navy">
	Any change that requires the pods to go down. This is similar to today with when you need to restart the JVM.  For example, applying a new custom archive with your customization.
	</span>

- **What databases are supported?.**

	<span style="color:navy">
	All three databases (Db2, Db2 Warehouse, Oracle and SQL server) are supported.
	</span>

- **What Industry Solution/Add-ons are supported?**

	<span style="color:navy">
	All Industry Solutions/Add-ons are supported. Scheduler, Calibration, Linear are included in Manage. Life Sciences is covered via Calibration.
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
	The API Key authentication is required for inbound HTTP/SOAP/REST-based integration to Manage. The API Key can be generated from the Manage app or REST API. The HTTP request header must include the API Key.
	</span>
    
	
- **What is the replacement of SI bus?**

	<span style="color:navy">
	Liberty JMS server, as well as Kafka community edition or any other supported JMS provider, are supported. Liberty JMS is available as a bundle from MAS config UI for any MAS Manage deployment.
	</span>

- **Is RMI supported?**

	<span style="color:navy">
	RMI is not supported outside of the Maximo server process. We recommend customers to leverage Maximo REST APIs instead of RMI. 
	
	RMI to Rest API: </span><https://www.youtube.com/watch?v=qY-xLlnmdI8>


- **Is BIRT reporting supported?**

	<span style="color:navy">Yes, BIRT is supported. Your reports will be moved automatically with the database upgrade.</span>


- **How to restart Manage server (other than deleting pods or restarting pods)?**

	<span style="color:navy">You can start and stop Manage server using tools-api.</span>
	
	- <span style="color:navy">Stop the Maximo Manage pods
		- POST </span> <https://host:port/toolsapi/toolservice/managestop>
	
	- <span style="color:navy">Start the Maximo Manage pods.
		- POST </span> <https://host:port/toolsapi/toolservice/managestart>
	
	<span style="color:navy">Detailed Instructions:</span>
		<https://www.ibm.com/support/pages/how-use-new-tools-api-maximo-application-suite>

- **How to deploy a custom Java class?**

	<span style="color:navy">
	The custom Java classes need to be packaged as a customization archive. A customization archive is a zip file and its structure is the same as the Maximo/SMP folder structure. It can include Java classes, XMLs, and database scripts. You need to follow the product.xml standard for customization. A customization archive is specified as part of the Manage CR spec so that the build process can include it. It can be accessed through the HTTP(s) or FTP(s) endpoint. Multiple customization archives are supported
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
	Cognos is not supported in MAS 8.8. It is in our roadmap for MAS 8.9.
	</span>

- **How is LDAP configured in MAS?**

	<span style="color:navy">MAS uses WebSphere Liberty to synchronize with LDAP. Liberty provides a SCIM API for MAS to consume the data from LDAP repositories into the MAS user registry. MAS pushes users/groups to Manage from MAS repository using user sync process.</span>
	
	<span style="color:navy">LDAP configuration:</span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=identity-ldap-user-registry-synchronization>


- **How is SMTP server configured?**

	<span style="color:navy">SMTP server is configured in MAS using MAS Admin UI.</span>
	
	<span style="color:navy">SMTP configuration: </span> <https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring-smtp-server>

- **How certificates can be applied?**

	<span style="color:navy">Cerificates can be applied from MAS Admin UI.</span>
	
	<span style="color:navy">Certificate configuration: </span> <https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-certificates>
	

- **What is the upgrade process?**

	<span style="color:navy">Upgrade Process: </span> <https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-upgrading-maximo-environment>

- **Are the Maximo users moved to MAS after upgrade?**

	<span style="color:navy">
	Yes, the Maximo users will be migrated to MAS from the existing Maximo (7612+) during the upgrade.</span>
	
	<span style="color:navy">Migrated Users: </span> <https://pages.github.ibm.com/maximo/manage-playbook/upgrade/users>


## Bug Fixes
- **How do I apply bug fixes?**

	- <span style="color:navy">Patches are periodically released with APAR fixes. It can be applied using MAS Admin UI manually or automatically if you have subscription.</span>
	
	- <span style="color:navy">LA(one-off) fixes can be applied using customization archieve.</span>


- **What is the rollback process when a patch fails at the app layer or the db layer**

	<span style="color:navy">
	The rollback process include:
	</span>
	
	- <span style="color:navy"> Roll back the configuration, which is the Manage Workspace CR and its associated secrets in the OpenShift Manage namespace.  The old image can be regenerated by the operator, or the old build can be specified to have the deployment point to revert back to what it was.</span>
	
	- <span style="color:navy"> Restore the database. (Same as 7.6)
	
	A new back-up and restore instruction document will be delivered in Manage 8.4. </span>

## EAM to Manage Gaps 

- **1.What are the EAM to Manage gaps?**

	<span style="color:navy">
	The following features/functionalities are not supported yet but are in the roadmap: 
	</span>
	
	- <span style="color:navy">Password controls/policy (password length, expiration date etc.) </span>	
	- <span style="color:navy">Disable/deactivate MAS user </span>
	- <span style="color:navy">Bulk user load in MAS </span>
	- <span style="color:navy">Bring your own certificate in MAS </span>
	- <span style="color:navy">MMI does not work for multiple servers </span>
	- <span style="color:navy">Not fully airgap enabled </span>

## Useful Links

<span style="color:navy">
Upgrading from IBM Maximo Enterprise Asset Management to IBM Maximo Manage:</span>

<https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=upgrading-from-maximo-enterprise-asset-management-maximo-manage>

<span style="color:navy">Manage in MAS:</span>

<https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-integration#concept_ecy_3dv_5tb>

<span style="color:navy">Maximo Application Suite:</span>

<https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring>

## Acronyms

| Abbreviations|Description|
|-------|----------|
|OCP| OpenShift Container Platform |
|MAS| Maximo Application Suite |
|CRD| Custom Resource Definition |
|CR| Custom Resouce|
|POD| Point of Deployment|


## Terminolgy

|Terminology|Description|
|-------|----------|
|OpenShift| OpenShift is the container platform that works with Kubernetes to help applications run more efficiently. The OpenShift container platform includes Kubernetes' platform and features (as well as Docker features). Kubernetes does not include OpenShift services, and it is its own standalone option, with its own unique Kubernetes dashboard.|
|Operator| Red Hat® OpenShift® Operators automate the creation, configuration, and management of instances of Kubernetes-native applications.|
|CRD| A CRD defines object kinds and lets the API Server handle the entire lifecycle.|
|CR| A CR is an object that extends the Kubernetes API. CR is the instance of CRD. |
|Deployment| OpenShift Container Platform deployments provide fine-grained management over common user applications. They are described using three separate API objects: 
||- A deployment configuration, which describes the desired state of a particular component of the application as a pod template
||- One or more replication controllers, which contain a point-in-time record of the state of a deployment configuration as a pod template.
||- One or more pods, which represent an instance of a particular version of an application. |
|POD| A POD is the core building block for running applications in a OpenShift cluster; a deployment is a management tool used to control the way pods behave.|
