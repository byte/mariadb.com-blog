# Automated server management with opensource tools

In a talk by Balazs Pocze, from Gawker Media LLC, it was made clear that there are many automation strategies for server management, that would be worth packaging up into an extended solution like [MariaDB Enterprise](https://mariadb.com/products/mariadb-enterprise). 

Automation is good because there are way less "ops people" than "dev people" at many companies. Man-hours are expensive, so you don't want to waste them on routine tasks. Automated tasks also mean that there is a lot less possibility to make mistakes. "Everybody needs automation," says Pocze.

Gawker still uses physical infrastructure, powered by Linux, though there is some migration to the cloud. [Cobbler](http://cobbler.github.io/) is their Linux installation server of choice, where the hosts are defined, and there is no manual DHCP or DNS management; this tool not only manages but also defines their environment. 

For provisioning the hosts, Gawker's tool of choice is [Puppet](https://puppet.com/). Puppet manages all the hosts as well as defines the hosts, and Pocze said, "If it doesn't exist in Puppet, it doesn't exist at all". From a developer enablement standpoint, MariaDB Enterprise provides the [MariaDB Enterprise Chef Cookbook](https://mariadb.com/kb/en/mariadb-enterprise/mariadb-enterprise-chef-cookbook/), which we could say is as close as can be.

In a bit of a twist, they also make use of [Ansible](https://www.ansible.com/) for running commands on hosts; all commands are organised into playbooks, and it is all about agentless installation and management. They do create modules and contribute them, and all nodes are managed over SSH. 

To wrap it all up, they use [Jenkins](https://jenkins.io/) for continuous integration. The demo of how Gawker's Kinja is maintained by Jenkins, with the Ansible playbooks for slave management was also a highlight.

It would be great if more shared what their backend infrastructure and ops ran like. Because its clear that there's plenty of opportunity to have tooling finesse. 

Don't forget to check out [banyek on github](https://github.com/banyek?tab=repositories) as well as [gawkermedia on github](https://github.com/gawkermedia/). During the talk, an audience member said it might also be a great idea to checkout [Rundeck - a job scheduler and runbook automation](http://rundeck.org/), something I have not heard of before but will definitely look at in the near future.