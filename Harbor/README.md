# Harbor_with_DevopsCube

##  What is Harbor?
Harbor is an open source registry that secures artifacts with policies and role-based access control, ensures images are scanned and free from vulnerabilities, and signs images as trusted. Harbor, a CNCF Graduated project, delivers compliance, performance, and interoperability to help you consistently and securely manage artifacts across cloud native compute platforms like Kubernetes and Docker.



##  Getting started
Harbor can be installed on any Kubernetes environment or on a system with Docker support. Information on how to get started:

## Installation Process
The standard Harbor installation process involves the following stages:
* ###  Harbor Installation Prerequisites.
   Harbor is deployed as several Docker containers. You can therefore deploy it on any Linux distribution that supports Docker. The target host requires Docker,  and Docker Compose to be installed.

  * #### Hardware
  
    The following table lists the minimum and recommended hardware configurations for deploying Harbor.

    | Resource | Minimum | Recommended |  
    |:-----------:|:-----------:|:-----------:|  
    | CPU  | 2 | 4 |  
    | Mem  | 4 | 8 |  
    | Disk | 40 | 160 |
  * #### Software
    The following table lists the software versions that must be installed on the target host.

    | Software | Version | Description |  
    |:-----------:|:-----------:|:-----------:|  
    | Docker engine  | Version 17.06.0-ce+ or higher | For installation instructions,<br/> see Docker Engine documentation |  
    | Docker Compose	  | docker-compose (v1.18.0+) or <br/> docker compose v2 <br/> (docker-compose-plugin)	 | For installation instructions,<br/> see Docker Compose documentation | 
    | Openssl | Latest is preferred	 | Used to generate certificate<br/> and keys for Harbor |
    
    
  * #### Network ports
     Harbor requires that the following ports be open on the target host.


    | Port | Protocol | Description |  
    |:-----------:|:-----------:|:-----------:|  
    | 443  | HTTPS | Harbor portal and core API accept<br/> HTTPS requests on this port.<br/> You can change this port in <br/>the configuration file.|  
    | 4443	  | HTTPS | Connections to the Docker Content<br/> Trust service for Harbor.<br/> Only required if Notary is enabled.<br/> You can change this port in the configuration file. | 
    | 80 | HTTP | Harbor portal and core API <br/>accept HTTP requests on this port.<br/> You can change this port in the <br/>configuration file. |



                

