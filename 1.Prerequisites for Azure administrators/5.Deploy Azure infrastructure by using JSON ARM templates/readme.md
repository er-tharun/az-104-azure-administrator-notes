# Deploy Azure infrastructure by using JSON ARM templates

## Introduction

- JSON Azure Resource Manager templates (ARM templates) allow you to specify your project's infrastructure in a declarative and reusable way. You can version and save the templates in the same source control as your development project.

> NOTE :
> Bicep is a language for defining your Azure resources. It has a simpler authoring experience than JSON, along with other features that help improve the quality of your infrastructure as code. We recommend that anyone new to infrastructure as code on Azure use Bicep instead of JSON. To learn about Bicep, see the Fundamentals of Bicep learning path.

### What is infrastructure as code?

- Infrastructure as code allows you to describe, through code, the infrastructure that you need for your application.

- With infrastructure as code, you can maintain both your application code and everything you need to deploy your application in a central code repository. The advantages to infrastructure as code are:

  - Consistent configurations
  - Improved scalability
  - Faster deployments
  - Better traceability

### What is an ARM template?

- ARM templates are JavaScript Object Notation (JSON) files that define the infrastructure and configuration for your deployment. The template uses a declarative syntax. The declarative syntax is a way of building the structure and elements that outline what resources look like without describing the control flow. Declarative syntax is different than imperative syntax, which uses commands for the computer to perform. Imperative scripting focuses on specifying each step in deploying the resources.
- ARM templates allow you to declare what you intend to deploy without having to write the sequence of programming commands to create it.
