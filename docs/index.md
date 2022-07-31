# Manage FAQs (MAS 8.8/Manage 8.5)

## What's new?

**OpenShift Operators:** The installation, configuration, deployment, the upgrade is performed by the OpenShift operator.

**Security & User Management:** The authentication and user management is configured in MAS. All users will be synchronized into Manage from MAS. All headless interactions (Integration, REST) require API Key for authentication.

**Application Server:** WebSphere Liberty will be used as a runtime to run the code in a containerized environment in Red Hat OpenShift. WebSphere ND and WebLogic are not supported. 

**Integration:** RMI is replaced by REST API.

**Message Queue:** If you are using SI Bus, you can use Liberty JMS server, Kafka or any other supported JMS provider.


## General
**Do the operators need a special configuration?**

Operators do not need any special configuration - their actions are driven by the CR (Custom Resource). Operators are the backbone of the automation in OpenShift/Kubernetes.  The operators’ configuration is provided by the administrator via the MAS/Manage admin UI.  Behind the scenes, this UI updates the CR (which can also be manually changed). The operators run as pods in the OCP cluster. 

**What is the use of the ingress controller?**


Ingress controller is OpenShift/Kubernetes means of exposing the service endpoint and load balancing to your applications. 

**What are the benefits of moving to OpenShift? More robust, quicker time to deliver infrastructure, do you already have a list?**
There are a number of items:
- Portability between cloud/on-prem environments
- Faster deployment compared to the traditional deployment model
- More robust, resilient, HA, and elasticity through containerization and container orchestration
- Consistency through the operator model, repeatable deployment 
- Capabilities for automating and streamlining the development process
 
**Can you please elaborate on ibm icr.io?**

It is IBM’s container registry. All IBM products’ images are stored there. The images are accessible if you purchased the product thus obtain an entitlement key. The entitlement key is to be provided when installing MAS, and the MAS and other application operators use this entitlement key to pull the images from icr.io. 
 
**For organizations that are on windows, are there options or only options to provision new RHEL envs /  move to cloud?**

You can run on bare metal or in VSphere.  See also https://docs.openshift.com/container-platform/4.7/installing/index.html#supported-platforms-for-openshift-clusters_ocp-installation-overview

**What is the one big limitation of moving to OpenShift?**

Potentially more hardware is needed for smaller installations
Short term learning curve (like any new technology)

**Are there specific requirements for a multi-tenancy environment?**

MT is not yet supported in OpenShift.

**Also OpenShift allows for dynamic scaling?**

Yes, but MAS is not fully there yet.

**Is the hypervisor something IBM provides or is that open source?**

There are different hypervisor products. Windows server datacenter solution provides windows hypervisor license. 

**Where does that plan into the diagram if you were to use windows?**

Windows is not supported at this time unless unsing sSphere
  
**What environment changes require application outages for users?**

Any change that requires the pods to go down.  This is similar to today with when you need to restart the JVM.  For example, applying a new custom archive with your customization. 


## Manage
**What databases are supported?.**

All three databases (Db2, Db2 Warehouse, Oracle and SQL server) are supported.

**What Industry Solution/Add-ons are supported?**

All Industry Solutions/Add-ons are supported. Scheduler, Calibration, Linear are included in Manage. Life Sciences is covered via Calibration.

**What languages are supported?**

All 23 languages are supported.

**Are Oracle and SAP integrations supported?**

Yes, Oracle and SAP integrations are supported.

**What are the supported authentication methods in MAS?**

The following authentication methods are supported:
- Local IDP (username/password registered in Mongo DB)
- LDAP
- SAML
https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring-authentication-methods

**What authentication is needed for inbound HTTP/SOAP/REST-based integration to Manage?**

The API Key authentication is required for inbound HTTP/SOAP/REST-based integration to Manage. The API Key can be generated from the Manage app or REST API. The HTTP request header must include the API Key.
    
**What is the replacement of SI bus?**

Liberty JMS server, as well as Kafka community edition or any other supported JMS provider, are supported. Liberty JMS is available as a bundle from MAS config UI for any MAS Manage deployment.

**Is RMI supported?**

RMI is not supported outside of the Maximo server process. We recommend customers to leverage Maximo REST APIs instead of RMI.
RMI to Rest API: https://www.youtube.com/watch?v=qY-xLlnmdI8 

**Is BIRT reporting supported?**

Yes, BIRT is supported. Your reports will be moved automatically with the database upgrade.

**How to restart Manage server (other than deleting pods or restarting pods)?**

You can start and stop Manage server using tools-api.
- Stop the Maximo Manage pods
POST https://host:port/toolsapi/toolservice/managestop 
- Start the Maximo Manage pods.
POST https://host:port/toolsapi/toolservice/managestart 
Detailed Instructions:
https://www.ibm.com/support/pages/how-use-new-tools-api-maximo-application-suite

**How to deploy a custom Java class?**

The custom Java classes need to be packaged as a customization archive. A customization archive is a zip file and its structure is the same as the Maximo/SMP folder structure. It can include Java classes, XMLs, and database scripts. You need to follow the product.xml standard for customization. A customization archive is specified as part of the Manage CR spec so that the build process can include it. It can be accessed through the HTTP(s) or FTP(s) endpoint. Multiple customization archives are supported.

**How do we access the System.Out logs for Maximo?**

Manage server logs are written to the standard output. You can view the logs from the OpenShift console.
- Go to your OpenShift console, navigate to the Workload/Pods menu, Select your Manage project.
- Check your Liberty server pods. Select the server pod to view log. 
You can also use toolsapi to upload and retrieve logs using S3 storage.
https://www.ibm.com/support/pages/how-use-new-tools-api-maximo-application-suite

**How can we run integrity checker?**

You can also use toolsapi to run integrity checker.

**How can we integrate Cognos with MAS?**

Cognos is not supported in MAS 8.8. It is in our roadmap for MAS 8.9.

**How is LDAP configured in MAS?**

MAS uses WebSphere Liberty to synchronize with LDAP. Liberty provides a SCIM API for MAS to consume the data from LDAP repositories into the MAS user registry. MAS pushes users/groups to Manage from MAS repository using user sync process.
https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=identity-ldap-user-registry-synchronization

**How is SMTP server configured?**

SMTP server is configured in MAS using MAS Admin UI. 
https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring-smtp-server

**How certificates can be applied?**

Cerificates can be applied from MAS Admin UI.
https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-certificates

**What is the upgrade process?**

https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-upgrading-maximo-environment

**Are the Maximo users moved to MAS after upgrade?**

Yes, the Maximo users will be migrated to MAS from the existing Maximo (7612+) during the upgrade.
https://pages.github.ibm.com/maximo/manage-playbook/upgrade/users

## Bug Fixes
**How do I apply bug fixes?**

- Patches are periodically released with APAR fixes. It can be applied using MAS Admin UI manually or automatically if you have subscription. 
- LA(One-off) fixes can be applied using customization archieve.

**What is the rollback process when a patch fails at the app layer or the db layer**

The rollback process include:
- Roll back the configuration, which is the Manage Workspace CR and its associated secrets in the OpenShift Manage namespace.  The old image can be regenerated by the operator, or the old build can be specified to have the deployment point to revert back to what it was.
- Restore the database. (Same as 7.6)
A new back-up and restore instruction document will be delivered in Manage 8.4.

## EAM to Manage Gaps 

**What are the EAM to Manage gaps?**

The following features/functionalities are not supported yet but are in the roadmap: 
- Password controls/policy (password length, expiration date etc.)
- Disable/deactivate MAS user
- Bulk user load in MAS
- Bring your own certificate in MAS
- MMI does not work for multiple servers
- Not fully airgap enabled

## Useful Links

Upgrading from IBM Maximo Enterprise Asset Management to IBM Maximo Manage
https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=upgrading-from-maximo-enterprise-asset-management-maximo-manage

Manage in MAS
https://www.ibm.com/docs/en/maximo-manage/continuous-delivery?topic=manage-integration#concept_ecy_3dv_5tb

Maximo Application Suite
https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring

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
- A deployment configuration, which describes the desired state of a particular component of the application as a pod template
- One or more replication controllers, which contain a point-in-time record of the state of a deployment configuration as a pod template.
- One or more pods, which represent an instance of a particular version of an application. |
|POD| A POD is the core building block for running applications in a OpenShift cluster; a deployment is a management tool used to control the way pods behave.|