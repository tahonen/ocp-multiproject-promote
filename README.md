# ocp-multiproject-promote
Multiproject image promotion templates with Slack integration and simple Jenkins pipelines

Goal is to provide simple Openshift project templates which you can use to create Development project for your application with proper build pipeline and Slack integation. 

With templates
* dev-template.yml
* test-template.yml
* prod-template.yml

You can bootstrap dev, test (also other envs between dev and prod) and prod projects for your fat jar application. Dev template contains hooks for unit tests and sonarqube static analysis and also Slack notifications. You just need Maven based Java app that createst fat jar...Springboot, Wildfly Swarm or Vert.x.

Production pipeline contains pipeline that first deploys new version using blue-green deployment and then A/B and finally fully releases new version to production.

## What you need

1. Openshift
2. Sonarqube running somewhere
3. Maven project in some git repo that is accessible from Openshift
4. Slack webhook URL and channel in Slack

## How to get started

You can get started by adding dev-template to your environment

```
oc create -f https://raw.githubusercontent.com/tahonen/ocp-multiproject-promote/master/dev-template.yml -n openshift
``` 
If you dont have write access to openshift project just leave '-n openshift' out from above command.

## Use newly created template

Open Product Catalog in Openshift and search for work 'dev'. You should see dev-environment in the search results. Click that and populate fields in the form

Here is sample sample values that you can use.
Service name: product-catalog
Enviroment name: dev
Promote tag: totest
Builder image: redhat-openjdk18-openshift
Builder image namespace: openshift
Buidler image version: latest
Branch: master
Repository address: https://github.com/tahonen/product-catalog.git
Slack webhook: Add your own 
Slack channek: Add your own
Wildcard DNS: Something like apps.example.com...
Sonarqube URL: URL to sonarqube http://sonarqube.pla.pla or OCP internal address http://sonarqube.internal-project.svc:9000

## Up next

Test and prod templates 
