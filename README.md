# An easy guide to design and implement a TOSCA template. 

Breve introduzione su cosa faremo

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
We have already seen an example of node type definition. We now dive deeper into this TOSCA type because 

### Example 

