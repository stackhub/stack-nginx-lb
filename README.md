# Purpose

Create a demonstrable, load balanced application stack with 
`nginx` as a load balancer using either `nginx` or `apache` as a backend.

# Usage

You will need to replace the environment variables for the `nginx-lb` 
service.  

* SE_API_TOKEN:  This is your Container Application Center (CAC) API Token. 
  It is used by `confd` to connect to the CAC Service Discovery layer.
* SE_LEADER_IP: The private IP address of the mesh leader.  
* SE_SERVICE_DISCOVERY_KEY: The portion of the service discovery 
  key to check for changes. Backends to `haproxy` are written based on 
  the values of these keys. (See below for how to construct them.)

## Constructing a Service Discovery Key and Range

The construction of a Service Discovery key is done as follows:

* {{application_instance_name}} + "-" + {{service_name}} + "-" 
  + {{exposed_ port}} 

TThe `application_instance_name` is what you set when clicking the
"Launch" button.

The `service_name` is defined when dragging a component into the editor 
graphically as the "Name".  It is also seen as the service name in the YAML.

The `exposed_port` is the _internally_ exposed port for the backend container. 
For both nginx and apache this will be 80.   

In the case of `nginx-apache.yml`, that would be the line reading 
"apache-backend-eg".

So, given that you name an application "nginx-lb-test" and the apache backends
"my-backend", and that nginx is listening on port 80 inside the container you 
would have the service discovery key:

`nginx-lb-test-my-backend-80` 

# Contributing

If you would like to contribute to this project, please follow the standard
fork-and-pr method.  

# License

MIT