#- [A practical guide about TOSCA](#a-practical-guide-about-TOSCA)
- [Something about the TOSCA standard.](#something-about-the-tosca-standard)
- [The general structure of a template.](#the-general-structure-of-a-template)
  - [Type definitions](#type-definitions)
  - [Topology template](#topology-template)
  - [Example of a simple TOSCA template](#example-of-a-simple-tosca-template)
- [TOSCA Types](#tosca-types)
  - [Data types](#data-types)
  - [Capability types](#capability-types)
  - [Interface types](#interface-types)
  - [Artifact types](#artifact-types)
  - [Relationship types](#relationship-types)
  - [Node types](#node-types)
- [Example](#example)

This is a guide about the TOSCA standard. We will explain its core features and its structure with a particular focus on type definitions. In the last section we will make an example of how to create a complete and modular template.  

## Something about the TOSCA standard. 
The TOSCA (Topology and Orchestration Specification for Cloud Applications) standard is a language-agnostic and platform-independent specification for describing cloud applications and their components, including their topology, relationships, and orchestration. It was developed by the OASIS (Organization for the Advancement of Structured Information Standards) consortium to address the challenges of deploying and managing complex, multi-tier cloud applications.

At its core, TOSCA provides a standardized way to describe the topology of a cloud application, including its components, relationships, and dependencies. This topology can be expressed in a TOSCA template, which is a YAML or XML file that describes the application's architecture. TOSCA templates can be used to automate the deployment and management of cloud applications, as well as define orchestration plans that specify how to manage and scale the application over its lifecycle.

TOSCA also provides a standard way to define relationships between components, which enables a more flexible approach to modeling and managing applications. For example, TOSCA allows for the definition of both horizontal and vertical scaling of an application, as well as the definition of policies that govern how the application should behave under different conditions.

TOSCA is designed to be platform-independent, meaning that it can be used to describe applications that run on any cloud platform. It is also language-agnostic, meaning that it can be used with any programming language or toolchain. This flexibility has made TOSCA a popular choice for managing complex cloud applications across a range of industries, including telecommunications, healthcare, and finance.

Overall, the TOSCA standard provides a powerful and flexible way to describe and manage cloud applications. It has gained widespread adoption in the industry and is supported by many cloud management and orchestration tools, making it an important standard for managing complex cloud environments.

## The general structure of a template. 
The general structure of a TOSCA template consists of the following sections:
- tosca_definitions_version. The TOSCA specification version used in the template, such as tosca_simple_yaml_1_3.
- imports. Url or path were to find TOSCA types to be included. 
- description. Brief description of the template.
- metadata. About the template, such as its name and version.
- data_types: This section defines any custom data types used in the template.
- artifact_types: This section defines any artifact types used in the template.
- capability_types: This section defines any capability types used in the template.
- interface_types: This section defines any interface types used in the template.
- relationship_types: This section defines any relationship types used in the template.
- node_types: This section defines any node types used in the template.
- group_types: This section defines any group types used in the template.
- policy_types: This section defines any policy types used in the template.
- topology_template. The topology of the application and the infrastructure requirements for each node.

Any yaml file containing al least one of these sections is considered a TOSCA template. 

Let's divide this sections in two main categories: **type definitions** and **topology template**. While the latter has its own section, the type definitions include all the sections ending with `_types`. 

### Type definitions
In TOSCA, type definition sections are used to define the types of various elements used in a TOSCA template. These type definitions can be reused and extended throughout the template, providing a way to create modular and composable templates that can be easily customized and adapted to different environments.

Some of the most common type definition sections in TOSCA are:
- data_types: This section defines the data types used in the TOSCA template, such as string, integer, boolean, or complex data types that can be composed of other data types. Data types can be used to define the types of properties and inputs for the node_templates and other elements in the TOSCA template.
- capability_types: This section defines the types of capabilities that a node_template can have, such as the ability to provide a database service, a load balancing service, or a web server service. Capability types define the properties, attributes, and interfaces that are required for the capability, and can be used to specify requirements for other node_templates that depend on the capability.
- interface_types: This section defines the types of interfaces that can be used by the node_templates in the TOSCA template, such as the ability to start or stop a service, or to perform other operations on the infrastructure. Interface types define the operations and input/output parameters that are required for the interface.
- artifact_types: This section defines the types of artifacts that can be used by the node_templates in the TOSCA template, such as software packages, scripts, or configuration files. Artifact types define the properties and attributes required for the artifact, and can be used to specify requirements for other node_templates that depend on the artifact.
- relationship_types: This section defines the types of relationships that can exist between node_templates, such as the ability of one node_template to provide a service to another node_template, or the ability of one node_template to depend on another node_template. Relationship types define the properties, attributes, and interfaces required for the relationship, and can be used to specify requirements and capabilities for the node_templates involved in the relationship.
- node_types: They are one of the most important type definitions in a TOSCA template. node_types define the properties, attributes, and behavior of a logical unit of infrastructure that can be deployed and managed using TOSCA. A node_type represents a class of infrastructure or application component that can be instantiated as a node_template in a TOSCA topology.

By defining and reusing these types in a TOSCA template, it becomes possible to create complex deployments that can be easily customized and adapted to different environments, while ensuring consistency and reliability across the deployment.

### Topology template
In a TOSCA template, the topology_template section defines the topology of the application or system being modeled. It describes how the different node_templates are connected and related to each other, forming a directed acyclic graph that represents the deployment topology. The topology_template section also contains other elements such as inputs, outputs, and workflows that help to define and manage the deployment.

The topology_template section has the following structure:
```yaml
topology_template:
  inputs:
    # Input parameter definitions
  node_templates:
    # Node template definitions
  groups:
    # Group definitions
  policies:
    # Policy definitions
  outputs:
    # Output parameter definitions
  workflows:
    # Workflow definitions
```
- inputs: This section contains the input parameter definitions for the TOSCA template. These parameters can be used to provide input values for the node_templates and workflows. Input parameters can have default values and constraints.
- node_templates: This section contains the definitions of the node_templates that make up the deployment topology. Each node_template represents a logical unit of infrastructure or application component that can be deployed and managed using TOSCA. The node_templates are connected to each other through relationship_templates, which describe the dependencies and connections between the node_templates.
- groups: This section contains the definitions of groups of node_templates that can be used to manage and orchestrate the deployment of multiple node_templates together. Groups can be used to define deployment policies, scaling policies, or other orchestration tasks.
- policies: This section contains the definitions of deployment policies that apply to the node_templates. Policies can define constraints, rules, or other criteria that govern the deployment and management of the node_templates.
- outputs: This section contains the output parameter definitions for the TOSCA template. These parameters can be used to provide output values from the node_templates and workflows.
- workflows: This section contains the definitions of workflows that can be used to orchestrate and automate deployment and management tasks for the node_templates. Workflows can be used to define deployment procedures, scaling procedures, or other automation tasks.

### Example of a simple TOSCA template
```yaml
tosca_definitions_version: tosca_simple_yaml_1_3

description: A simple TOSCA template with two linked nodes

data_types:
  my_type:
    derived_from: string

node_types:
  my_node_type:
    properties:
      my_property:
        type: my_type
    capabilities:
      my_capability:
        type: tosca.capabilities.Node
    requirements:
      - my_requirement:
          capability: my_capability
          node: my_node_type

topology_template:
  inputs:
    my_input:
      type: my_type
  node_templates:
    my_node:
      type: my_node_type
      properties:
        my_property: { get_input: my_input }
      capabilities:
        my_capability:
          properties:
            key: value
      requirements:
        - my_requirement:
            node: my_other_node
    my_other_node:
      type: my_node_type
      properties:
        my_property: another_value
```
In this example, we start by defining a data type called `my_type`, which is derived from the built-in string type.

Next, we define a node type called `my_node_type`, which has a property called `my_property` of type `my_type`, a capability called `my_capability` of type `tosca.capabilities.Node`, and a requirement called `my_requirement` that specifies that the node requires another node of type `my_node_type` that has the `my_capability`.

In the topology_template section, we define an input called `my_input` of type `my_type`. We then define two node templates, `my_node` and `my_other_node`, both of which are of type `my_node_type`.

`my_node` has a property called `my_property` that is set to the value of the `my_input` input, a capability of type `my_capability` with a property called key set to value, and a requirement for `my_other_node`.

`my_other_node` has a property called `my_property` set to another_value.

The requirement and capability specified in the node templates create a relationship between `my_node` and `my_other_node`. This ensures that `my_other_node` is started before the `my_node` node because when a TOSCA service template is executed, the orchestrator will first create and configure the nodes that have no dependencies. Once those nodes are up and running, the orchestrator will create and configure the nodes that depend on the previously created nodes.

## TOSCA Types
The TOSCA standard strongly relies on the concept of tosca type. In TOSCA, a type is a reusable definition that defines the properties, attributes, and behavior of a certain kind of entity, such as a node, capability, interface, or relationship. Types are used to define the building blocks of TOSCA templates, and they are defined in the data_types, capability_types, interface_types, relationship_types, and node_types sections of a TOSCA template.

Each type has a name and a set of properties, which can have data types, default values, and constraints. Types can also have derived_from relationships, which allow them to inherit properties and behavior from other types. This allows TOSCA types to be organized into hierarchies, where more specific types can inherit from more general types and add or override properties as needed. TOSCA also provides some basics types for each category named using this convention `tosca.<cathegory>.<name>` such as `tosca.capabilities.OperatingSystem`, `tosca.artifacts.Implementation` or `tosca.nodes.Compute`. 

TOSCA types are designed to be reusable and composable, which means that they can be combined and reused across different TOSCA templates and applications. This helps to reduce duplication, promote consistency, and improve maintainability of TOSCA templates and applications. 
Usually you will write a template where you only define all of your needed and shared custom types to be imported into other definitions. 

Now we will briefly explain each type capabilities with examples. 

### Data types 
In TOSCA, data types are used to define a set of properties and their types that can be used in node templates and other sections of a TOSCA service template. A data type can be defined as a complex type, which can include a set of simple types, or as a simple type, which is a single data type. Data types are important in TOSCA because they provide a way to define the structure and constraints of the data that will be used to configure and operate nodes in a TOSCA deployment. 

In TOSCA, the basic data types that are provided out of the box are:
- string: A sequence of characters that can include letters, numbers, and symbols.
- integer: A whole number without decimals.
- float: A number with decimal places.
- boolean: A value that is either true or false.
- timestamp: A date and time expressed in a standardized format.
- version: A version number that follows the Semantic Versioning specification.

In addition to the basic types, TOSCA provides also two collection types
- list: An ordered array of properties. It can contain both basic and custom data types. It represents the equivalent of `std::vector` in C++ or `List` in Python. 
- map: A map of properties defined by name. It must define an entry_schema section to set the type its made of. It is the equivalent of hash tables in standard programming languages. 

This is an example of custom data type definition which represents and IPv4 or IPv6 address: 
```yaml
data_types:
  IPAddress:
    derived_from: tosca.datatypes.string
    constraints:
      - pattern: ^([0-9]{1,3}\.){3}[0-9]{1,3}$|^([0-9a-fA-F]{1,4}:){7}[0-9a-fA-F]{1,4}$
```
It derives from the `string` basic type and its values are constrained to match the regular expression pattern to represent an IP address. 

### Capability types
In TOSCA, a capability represents a named, typed set of properties that a node can provide or require. Capability types define the structure and properties of capabilities that can be used in a TOSCA service template. They provide a way to abstract the capabilities of nodes, allowing them to be reused across different node types. 

This is an example of capability type: 
```yaml
  tosca.capabilities.indigo.OperatingSystem:
    derived_from: tosca.capabilities.OperatingSystem
    properties:
      gpu_driver:
        type: boolean
        required: no
      cuda_support:
        type: boolean
        required: no
      cuda_min_version:
        type: string
        required: no
      cuDNN_version:
        type: string
        required: no
      image:
        type: string
        required: no
      credential:
        type: tosca.datatypes.Credential
        required: no
```
In this case, it is a derived capability type called tosca.capabilities.example.OperatingSystem, which is derived from the built-in tosca.capabilities.OperatingSystem capability type.

This derived capability type defines several new properties such as `gpu_driver, cuda_support`, `cuda_min_version`, `cuDNN_version`, `image`, and `credential`. Each property has a type and an optional required field. For example, the credential property has a type of `tosca.datatypes.Credential` and is not marked as required, which means it can be omitted when using this capability type.

### Interface types
TOSCA interface types define a set of operations that can be performed on a node or relationship. An interface type can be defined at the node or relationship level, or it can be defined as a separate type and then referenced by multiple nodes or relationships. Each operation is defined by a set of inputs and outputs, and can be implemented by a script or other executable code.

Interface types are an important component of TOSCA because they provide a way to standardize the way that different nodes and relationships can be operated. This allows users to perform the same operations on different types of nodes or relationships using a consistent interface. For example, an interface type could be defined to start, stop, and restart a web server, which could be used with different web server implementations.

There are several built-in interface types in TOSCA, including tosca.interfaces.node.lifecycle.Standard, which defines a standard set of lifecycle operations for a node, such as create, configure, start, stop, and delete.

Custom interface types can also be defined using YAML, with each operation defined by a set of inputs, outputs, and an implementation. For example, an interface type could be defined to backup and restore a database, with inputs for the database name and backup location, and outputs for the backup status. The implementation could be a script that performs the backup and restore operations using the specified inputs and outputs.

This is an example of custom Interface type definition for deploying a Docker container: 
```yaml
tosca.interfaces.docker:
  derived_from: tosca.interfaces.Root
  description: Interface for deploying Docker containers
  inputs:
    image_name:
      type: string
      description: The name of the Docker image to deploy
      required: true
    container_name:
      type: string
      description: The name to assign to the Docker container
      required: true
    ports:
      type: list
      entry_schema:
        type: string
      description: The ports to expose on the container
      required: false
  operations:
    create:
      description: Create a Docker container
      implementation: docker_create.sh
      inputs:
        image_name:
          type: string
          value: { get_input: image_name }
        container_name:
          type: string
          value: { get_input: container_name }
        ports:
          type: list
          value: { get_input: ports }
    start:
      description: Start a Docker container
      implementation: docker_start.sh
      inputs:
        container_name:
          type: string
          value: { get_input: container_name }
    stop:
      description: Stop a Docker container
      implementation: docker_stop.sh
      inputs:
        container_name:
          type: string
          value: { get_input: container_name }

```
In this example, we're defining a custom interface type called `tosca.interfaces.docker`, which is used for deploying Docker containers. The interface type includes three input parameters, which are used to configure the deployment of the container: `image_name`, `container_name`, and `ports`. The `image_name` parameter is a required string that specifies the name of the Docker image to deploy. The `container_name` parameter is also a required string that specifies the name to assign to the Docker container. The ports parameter is an optional list of string values that specifies the ports to expose on the container.

The interface type also includes three operations: `create`, `start`, and `stop`. The `create` operation creates a new Docker container using the specified image name and container name, and exposes any ports specified in the ports input parameter. The `start` operation starts an existing Docker container with the specified container name, and the `stop` operation stops a running Docker container with the specified container name.

Each operation has a description, an implementation script (in this example, `docker_create.sh`, `docker_start.sh`, and `docker_stop.sh`), and input parameters that are mapped to the corresponding input parameters defined in the interface type. For example, the create operation maps the `image_name`, `container_name`, and `ports` input parameters to the corresponding input parameters defined in the interface type using the `get_input` function. This allows the operations to use the input parameter values specified when the interface is invoked, enabling dynamic configuration of the Docker container deployment.

### Artifact types
In TOSCA, an artifact is a piece of content that is used by a node or other resource within a service template. Artifact types define the structure and properties of artifacts that can be used in a TOSCA service template. TOSCA includes several built-in artifact types, such as `tosca.artifacts.File`, which can be used to represent a file artifact. Each artifact type includes a set of defined properties, such as file, which specifies the location of the artifact on the file system.

This is an example which represents a YAML Ansible recipe artifact: 
```yaml 
  tosca.artifacts.Implementation.YAML:
    derived_from: tosca.artifacts.Implementation
    description: YAML Ansible recipe artifact
    mime_type: text/yaml
    file_ext: [ yaml, yml ]
```

### Relationship types
In TOSCA, Relationship types define the nature of the relationship between two nodes in a topology. A Relationship type specifies the interface and operations that a target node can provide to its source node. Relationship types can be used to model dependencies between nodes, such as a web server that depends on a database.

Relationship types can be either built-in or custom-defined. Built-in Relationship types are predefined and provided by the TOSCA specification, while custom-defined Relationship types can be created by the user to represent specific relationships between nodes.

The TOSCA Relationship type hierarchy includes two base types: the tosca.relationships.Root type, which serves as the parent for all Relationship types, and the tosca.relationships.DependsOn type, which is used to represent a simple dependency between nodes.

Custom-defined Relationship types can derive from any built-in Relationship type or another custom-defined Relationship type, and can define their own properties and interfaces. Relationship types can also specify requirements and capabilities that the source and target nodes must have in order to establish the relationship.

This is an example of a custom relationship type definition: 
```yaml
relationship_types:
  mycompany.relationships.depends_on:
    derived_from: tosca.relationships.DependsOn
    description: This relationship type represents a dependency between two nodes.
    valid_target_types: [tosca.nodes.Compute, tosca.nodes.Storage]
    properties:
      timeout:
        type: integer
        description: The number of seconds to wait for the dependency to become available.
        default: 60
    interfaces:
      mycompany.interfaces.depends_on:
        description: This interface defines operations for managing dependencies between nodes.
        operations:
          add_dependency:
            description: Adds a dependency between the source and target nodes.
            inputs:
              dependency_type:
                type: string
                description: The type of dependency, such as "hard" or "soft".
                default: hard
              timeout:
                type: integer
                description: The number of seconds to wait for the dependency to become available.
                default: 60
          remove_dependency:
            description: Removes a dependency between the source and target nodes.
            inputs:
              dependency_type:
                type: string
                description: The type of dependency to remove.
                default: hard

```
In this example, we define a custom relationship type called `mycompany.relationships.depends_on`, which is derived from the built-in `tosca.relationships.DependsOn` type. We also define a set of properties for the relationship, including a timeout property that specifies the number of seconds to wait for the dependency to become available.

We also define a custom interface for the relationship type, called `mycompany.interfaces.depends_on`, which includes two operations: `add_dependency` and `remove_dependency`. Each operation includes a set of inputs, such as the `dependency_type` and timeout inputs for the add_dependency operation.

### Node types
In TOSCA, a node type defines a specific kind of software or hardware component that can be deployed as part of an application topology. A node type can include information about the properties, attributes, and capabilities of the node, as well as any requirements it may have for deployment. For example, a node type could represent a web server, a database, or a load balancer.

Node types can be defined in a TOSCA template using YAML syntax. They are typically derived from a parent node type, which can be a built-in TOSCA node type or a custom node type defined in the template. The properties of a node type can include metadata, constraints, and default values, and can be used to specify any relevant configuration data for the node.

In addition to properties, node types can include capability types, which define the specific capabilities that the node provides, and requirement types, which define the specific requirements that the node has for deployment. For example, a web server node type might include a capability type for serving web pages and a requirement type for a load balancer to distribute incoming requests.

Overall, node types are a key component of TOSCA because they enable the definition and deployment of complex application topologies that consist of many different software and hardware components. By defining node types in a TOSCA template, developers can ensure that each component is deployed correctly and configured to work seamlessly with other components in the topology.

This is an example of customized node type. In particular, this is the implementation of the indigo Compute node. This definition and other Indigo basic types can be found [here](https://baltig.infn.it/infn-cloud/tosca-types/-/blob/master/tosca_types/base/basic_types.yaml). 

```yaml
   tosca.nodes.indigo.Compute:
    derived_from: tosca.nodes.Compute
    metadata:
      icon: /images/compute.png
    attributes:
      private_address:
        type: list
        entry_schema:
          type: string
      public_address:
        type: list
        entry_schema:
          type: string
      ctxt_log:
        type: string
    properties:
      os_users:
        type: list
        description: Users creation
        entry_schema:
          type: tosca.datatypes.indigo.User
        default: []
        required: false
      tags:
        type: map
        description: Map of tags to associate to the Compute instance
        entry_schema:
          type: string
        default: {}
        required: false  
      fail2ban_enabled: 
        type: boolean
        default: true
      fail2ban_bantime: 
        type: integer
        default: 200
      fail2ban_maxretry: 
        type: integer
        default: 10
      fail2ban_jail_config:
        type: string
        default: |
          - option: 'enabled'
            value: 'true'
            section: 'sshd'
          - option: 'action'
            value: '%(action_)s'
            section: DEFAULT
    capabilities:
      scalable:
        type: tosca.capabilities.indigo.Scalable
      os:
         type: tosca.capabilities.indigo.OperatingSystem
      endpoint:
        type: tosca.capabilities.indigo.Endpoint
      host:
        type: tosca.capabilities.indigo.Container
        valid_source_types: [tosca.nodes.SoftwareComponent]
    artifacts:
      os_users_role:
        file: indigo-dc.os_users
        type: tosca.artifacts.AnsibleGalaxy.role
      security_role:
        file: maricaantonacci.security
        type: tosca.artifacts.AnsibleGalaxy.role
    interfaces:
      Standard:
        configure:
          implementation: https://raw.githubusercontent.com/indigo-paas/tosca-types/main/artifacts/os/configure_system.yml
          inputs:
            os_users: { get_property: [ SELF, os_users] }
            security_fail2ban_enabled: { get_property: [ SELF, fail2ban_enabled ] }
            security_fail2ban_bantime: { get_property: [ SELF, fail2ban_bantime ] }
            security_fail2ban_maxretry: { get_property: [ SELF, fail2ban_maxretry ] }
            fail2ban_jail_configuration: { get_property: [ SELF, fail2ban_jail_config ] }
```
In the example above, we have a custom TOSCA Node Type called "tosca.nodes.indigo.Compute". This Node Type is derived from the TOSCA Compute Node Type and adds additional properties, attributes, capabilities, and interfaces that are specific to the Indigo project.

For example, the "os_users" property is a list of users that will be created on the Compute instance, and the "tags" property is a map of tags that will be associated with the instance. The Node Type also includes a "scalable" capability that allows the instance to be scaled up or down, an "os" capability that specifies the operating system of the instance, an "endpoint" capability that provides information about the network endpoints exposed by the instance, and a "host" capability that specifies that the instance can host other nodes.

The Node Type also includes two artifacts, "os_users_role" and "security_role", that are Ansible Galaxy roles used to configure the instance, and a Standard interface with a "configure" operation that uses an Ansible playbook to configure the instance with the specified properties and attributes. Overall, the TOSCA Node Type provides a flexible and reusable way to define the Compute nodes in the Indigo project.

## Example 
Now we can put all the things together and write a complete TOSCA template. 

In this example we will deploy a web server and a database, with user input to choose the operating system:

```yaml 
tosca_definitions_version: tosca_simple_yaml_1_3

description: Example TOSCA template for deploying a web server and a database

metadata:
  template_name: web-server-database-template

inputs:
  vm_flavors:
    type: list
    description: List of available virtual machine flavors
    entry_schema:
      type: string

node_types:
  my.company.nodes.WebServer:
    derived_from: tosca.nodes.WebServer
    properties:
      web_content:
        type: string
        required: true
    requirements:
      - host:
          capability: my.company.capabilities.Compute
          node: my.company.nodes.Compute

  my.company.nodes.Database:
    derived_from: tosca.nodes.Database
    properties:
      db_name:
        type: string
        required: true
      db_user:
        type: string
        required: true
      db_password:
        type: string
        required: true
    requirements:
      - host:
          capability: my.company.capabilities.Compute
          node: my.company.nodes.Compute

  my.company.nodes.Compute:
    derived_from: tosca.nodes.Compute
    properties:
      flavor:
        type: string
        required: true
        default: { get_input: vm_flavors }

  my.company.capabilities.Compute:
    derived_from: tosca.capabilities.Compute

topology_template:
  inputs:
    web_content:
      type: string
      description: Content to be served by the web server
      default: "Hello, World!"

  node_templates:
    web_server:
      type: my.company.nodes.WebServer
      properties:
        web_content: { get_input: web_content }
      requirements:
        - host: { node: compute }

    database:
      type: my.company.nodes.Database
      properties:
        db_name: my_db
        db_user: my_user
        db_password: my_password
      requirements:
        - host: { node: compute }

    compute:
      type: my.company.nodes.Compute
      properties:
        flavor: { get_input: vm_flavors }
```

In this template, we have defined three custom node types (`my.company.nodes.WebServer`, `my.company.nodes.Database`, and `my.company.nodes.Compute`) that are derived from the TOSCA built-in node types. We have also defined a custom capability type `my.company.capabilities.Compute` that is derived from the `tosca.capabilities.Compute` built-in capability type.

The inputs section defines an input called `vm_flavors`, which is a list of available virtual machine flavors. This input can be set by the user when deploying the template.

In the `node_templates` section, we have defined three node templates: `web_server`, `database`, and `compute`. The `web_server` node is of type `my.company.nodes.WebServer`. The `database` node is of type `my.company.nodes.Database`. They both require a host that provides the `my.company.capabilities.Compute` capability. The compute node is of type `my.company.nodes.Compute` and provides the `my.company.capabilities.Compute` capability. In this way it is possible to host on the `compute` node, both the web server and the database. 

The `web_server` node is defined as an instance of the `tosca.nodes.WebServer` node type, which is derived from the `tosca.nodes.SoftwareComponent` node type. The node has a single capability of type `tosca.capabilities.Endpoint`, which defines a single port (port 80) for accessing the web server. The node also has an input property called `os_flavor` which allows the user to select the operating system flavor to use for the virtual machine.

The database node is defined as an instance of the `tosca.nodes.Database` node type, which is also derived from the `tosca.nodes.SoftwareComponent` node type. The node has a single capability of type `tosca.capabilities.Database`, which defines the database endpoint and credentials. The node also has an input property called `db_flavor` which allows the user to select the database flavor to use.

The relationship between the web server and the database nodes is defined as an instance of the `tosca.relationships.ConnectsTo` relationship type. This relationship specifies that the web server node requires the database node to be started before it can be started.

Finally, the topology template specifies a single node template that instantiates both the web server and the database nodes, and defines the inputs for the `os_flavor` and `db_flavor` properties.

To make reusable the defined types and to keep the template cleaner and more readable, it is possible to move their definitions in a different file and then import it with the import section of the template. 
When it comes to design a complex TOSCA infrastructure with many different tosca types as service to be deployed and reused, it is usually a good idea to create two repositories, one for type definitions, and another one for topological templates. 

The TOSCA-type repository has a directory structure like this: 

```
.
├── artifacts
└── tosca_types
    ├── base
    │    └── basic_types.yaml 
    └── applications
         ├── application_1.yaml 
         ├── application_2.yaml 
         └── application_3.yaml 
```
The `artifacts` folder contains the artifacts (such as ansible roles, configurations scrips and so on) needeed from the templates. The `tosca_types` folder is branched in a `base` folder and a `applications` folder. 
In the `base` folder there is a `basic_types.yaml` template which contains the definition of types shared among the various applications. In the `application` folder, instead, there are the definitions of specific TOSCA types which are reused in different templates but not shared among the applications. 

The TOSCA-template repository, instead, contains topological templates, which uses both the basic types and the application types. They are clean and focused on the gathering of the user inputs and management of the topology of the infrastructure. 


