###########
jenkinslint
###########

A basic Jenkinsfile linter (validator). Can validate files using a Jenkins web
interface, or the Jenkins SSH interface.

.. image:: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white
   :target: https://github.com/pre-commit/pre-commit
   :alt: pre-commit

Usage
=====

To configure which type of validation to use (web or SSH), create an INI file
named ``.jenkinslintrc`` in the root of your repository.

The following parameters are supported:

JENKINS_SERVER
   Server name

JENKINS_SSH_PORT
   When set, use SSH validation

JENKINS_UNSAFE_SSL
   When set to TRUE, disable SSL/TLS certificate validation

JENKINS_URL
   Full Jenkins URL for web-based validation
   
DEBUG
   If set to true, display all logs (Even if lint is successful)

Not all parameters need to be set. Example:

::

   JENKINS_SERVER=jenkins.demo.local
   JENKINS_SSH_PORT=8022

Standalone
----------

Validate files using ``jenkinslint`` followed by the name of the Jenkinsfile,
e.g.

::

   jenkinslint Jenkinsfile

Using the pre-commit framework
------------------------------

Install the pre-commit framework, and add the following to the
``.pre-commit-config.yaml`` file:

::

    - repo: https://github.com/Ouisticram/jenkinslint
      rev: v1.1.3
      hooks:
       - id: jenkinslint
         name: Lint Jenkinsfile
         description: Validates Jenkinsfiles using a Jenkins server
         files: .*Jenkinsfile
         require_serial: true

This will automatically validate files named ``Jenkinsfile`` during the pre
commit phase.

