# Jenkins on DC/OS
[![Build Status](https://jenkins.mesosphere.com/service/jenkins/buildStatus/icon?job=Jenkins/public-jenkins-dcos-master)](https://jenkins.mesosphere.com/service/jenkins/view/Velocity/job/Jenkins/job/public-jenkins-dcos-master/)
[![Docker Stars](https://img.shields.io/docker/stars/mesosphere/jenkins.svg)][docker-hub]
[![Docker Pulls](https://img.shields.io/docker/pulls/mesosphere/jenkins.svg)][docker-hub]
[![](https://images.microbadger.com/badges/image/mesosphere/jenkins.svg)](http://microbadger.com/images/mesosphere/jenkins "Get your own image badge on microbadger.com")

Run a Jenkins master on DC/OS, using Docker and Nginx. This Jenkins instance is pre-configured to autoscale build agents onto the DC/OS cluster using the [Jenkins Mesos plugin][mesos-plugin].

## Overview
This repo contains a [Dockerfile](Dockerfile) that runs Jenkins inside a Docker
container and uses [Nginx][nginx-home] as a reverse proxy. It also provides
several Jenkins plugins and a basic Jenkins configuration in order to get you
up and running quickly with Jenkins on DC/OS.

## Reporting issues

Please report issues and submit feature requests for Jenkins on DC/OS by [creating an issue in the DC/OS JIRA][dcos-jira] (JIRA account required).

## Included in this repo
Base packages:
  * [Jenkins][jenkins-home] 2.46.2 (LTS)
  * [Nginx][nginx-home] 1.10.1

Jenkins plugins:
  * ace-editor v1.1
  * ansicolor v0.5
  * ant v1.4
  * antisamy-markup-formatter v1.5
  * artifactory v2.10.4
  * async-http-client v1.7.24.1
  * authentication-tokens v1.3
  * aws-credentials v1.16
  * aws-java-sdk v1.11.37
  * azure-slave-plugin v0.3.4
  * blueocean v1.0.1
  * blueocean-commons v1.0.1
  * blueocean-config v1.0.1
  * blueocean-dashboard v1.0.1
  * blueocean-events v1.0.1
  * blueocean-git-pipeline v1.0.1
  * blueocean-github-pipeline v1.0.1
  * blueocean-jwt v1.0.1
  * blueocean-personalization v1.0.1
  * blueocean-pipeline-api-impl v1.0.1
  * blueocean-rest v1.0.1
  * blueocean-rest-impl v1.0.1
  * blueocean-web v1.0.1
  * bouncycastle-api v2.16.0
  * branch-api v2.0.9
  * build-name-setter v1.6.5
  * build-timeout v1.18
  * cloudbees-folder v6.0.4
  * conditional-buildstep v1.3.5
  * config-file-provider v2.15.7
  * copyartifact v1.38.1
  * credentials v2.1.7
  * credentials-binding v1.9
  * cvs v2.13
  * display-url v0.5
  * docker-build-publish v1.3.2
  * docker-commons v1.5
  * docker-workflow v1.10
  * durable-task v1.13
  * ec2 v1.36
  * embeddable-build-status v1.9
  * external-monitor-job v1.7
  * favorite v1.16
  * ghprb v1.36.2
  * git v3.3.0
  * git-client v2.4.5
  * git-server v1.7
  * github v1.27.0
  * github-api v1.85
  * github-branch-source v2.0.5
  * github-organization-folder v1.6
  * gitlab v1.4.5
  * gradle v1.26
  * greenballs v1.15
  * handlebars v1.1.1
  * icon-shim v2.0.3
  * ivy v1.27.1
  * jackson2-api v2.7.3
  * javadoc v1.4
  * job-dsl v1.61
  * jobConfigHistory v2.16
  * jquery v1.11.2-0
  * jquery-detached v1.2.1
  * junit v1.19
  * ldap v1.15
  * mailer v1.18
  * mapdb-api v1.0.9.0
  * marathon v1.4.0
  * matrix-auth v1.5
  * matrix-project v1.10
  * maven-plugin v2.15.1
  * mesos v0.14.1
  * metrics v3.1.2.9
  * momentjs v1.1.1
  * monitoring v1.65.1
  * nant v1.4.3
  * node-iterator-api v1.5.0
  * pam-auth v1.3
  * parameterized-trigger v2.33
  * pipeline-build-step v2.5
  * pipeline-github-lib v1.0
  * pipeline-input-step v2.7
  * pipeline-milestone-step v1.3.1
  * pipeline-model-definition v1.1.4
  * pipeline-rest-api v2.6
  * pipeline-stage-step v2.2
  * pipeline-stage-view v2.6
  * plain-credentials v1.4
  * rebuild v1.25
  * role-strategy v2.4.0
  * run-condition v1.0
  * s3 v0.10.12
  * saferestart v0.3
  * saml v0.13
  * scm-api v2.1.1
  * script-security v1.24
  * sse-gateway v1.10
  * ssh-agent v1.15
  * ssh-credentials v1.12
  * ssh-slaves v1.17
  * structs v1.5
  * subversion v2.7.2
  * support-core v2.33
  * timestamper v1.8.8
  * token-macro v2.0
  * translation v1.15
  * variant v1.1
  * windows-slaves v1.3.1
  * workflow-aggregator v2.5
  * workflow-api v2.13
  * workflow-basic-steps v2.4
  * workflow-cps v2.30
  * workflow-cps-global-lib v2.8
  * workflow-durable-task-step v2.11
  * workflow-job v2.10
  * workflow-multibranch v2.14
  * workflow-scm-step v2.4
  * workflow-step-api v2.9
  * workflow-support v2.14

## Packaging
Jenkins is available as a package in the [Mesosphere Universe][universe].
To make changes to the Jenkins package, submit a pull request against the
Universe.

## Installation

To install Jenkins for the DC/OS, simply run `dcos package install jenkins` or install via the Universe page in the DC/OS UI.

Jenkins should now be available at <http://dcos.example.com/service/jenkins>.
See [Getting Started][getting-started] for more in-depth instructions and
configuration options.

## Releasing
To release a new version of this package:

  1. Update [the Jenkins conf][jenkins-conf] to reference the current release of
  the [jenkins-dind][jenkins-dind] Docker image (if needed).
  2. Add some release notes to [CHANGELOG.md](CHANGELOG.md)
  3. Tag the commit on master that you want to be released.
  4. Once [the build][jenkins-build] has successfully completed, submit a new
  pull request against [the Universe][universe] referencing the new tag.

[dcos-jira]: https://jira.mesosphere.com/secure/CreateIssueDetails!init.jspa?pid=14110&issuetype=3
[docker-hub]: https://hub.docker.com/r/mesosphere/jenkins
[getting-started]: https://docs.mesosphere.com/latest/usage/service-guides/jenkins/
[jenkins-conf]: /conf/jenkins/config.xml
[jenkins-dind]: https://github.com/mesosphere/jenkins-dind-agent
[jenkins-home]: https://jenkins-ci.org/
[mesos-plugin]: https://github.com/jenkinsci/mesos-plugin
[nginx-home]: http://nginx.org/en/
[jenkins-build]: https://jenkins.mesosphere.com/service/jenkins/job/public-jenkins-dcos-master/
[universe]: https://github.com/mesosphere/universe
