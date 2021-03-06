# Azure DevOps: self-service creation of a new Azure DevOps project

## Presentation

This article explains how you can set up a self-service mechanism to allow people in your org to create a new project and get the project being automatically configured from a "templated" one (scaffolding of repo, RBAC, pipeline, branching, etc).

## Context

In large companies, there is often one central team responsible to provide services to the developers, like a software factory platform. When they are using Azure DevOps, they generally create one Azure DevOps organization and then create one project per team or per project. They are the only ones with enough rights to create projects and so, other teams have to go through them every time they want a new project.

## Today

There are different ways to handle the creation of the project and of course, it depends on the actual process in place in the company. Sometimes, teams just send an email, sometimes they have to create a ServiceNow ticket, sometimes they need to bribe the team to get a project canvas. There is one common process:
Dev team --> new demand --> send to AzureDevOps team --> manual creation of the project

There are pros and cons in this very simple process

### pros

- centralized demand system
- possibility of implementing specific controls/validation

### cons

- slow project creation
- time-consuming for the Azure DevOps teams
- not very reactive (only during work hours)
- not scalable when dozen of demands
- not "DevOps"-mindset (not using automatization when possible)

## Tomorrow

What I'm showing here is how to automate a big part of the process, from receiving the demand to create a project and at the same time scaffold some good practices.

There are of course different ways of doing it. I could implement a chatbot experience to build a conversational agent to receive the demand. I could also develop my custom self-service portal. In both cases, it requires custom development and for each evolution, it would require to rewrite/redeploy my app. I could, but I won't! Instead, **I would like to leverage Azure DevOps as much as possible** to be flexible but also not to require external infrastructure to maintain.

My solution is:

1. using Azure DevOps as a [ticketing system](./ticketing/readme.md) (could be replaced easily by Jira, ServiceNow or anything else with an exposed Rest API, or even a mailbox)
2. using Azure DevOps pipeline to drive the [creation of the project](./creation/readme.md)
3. using Microsoft Flow to [monitor and process the tickets](./processing/readme.md) and create controls
4. (optional) to add some [improvments](./improvements/readme.md) on my project template
