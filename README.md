# Ansible Role: Jenkins CI for Windows

Installs Jenkins CI on windows servers.

## Requirements

Requires `curl` and `Java` to be installed on the server.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    jenkins_hostname: localhost

The system hostname; usually `localhost` works fine. This will be used during setup to communicate with the running Jenkins instance via HTTP requests.

    jenkins_home: C:\program files\jenkins

The Jenkins home directory which, amongst others, is being used for storing artifacts, workspaces and plugins. This variable allows you to override the default `C:\program files\jenkins` location.

    jenkins_http_port: 8080

The HTTP port for Jenkins' web interface.

    jenkins_admin_username: admin
    jenkins_admin_password: admin

Default admin account credentials which will be created the first time Jenkins is installed.

    jenkins_admin_password_file: ""

Default admin password file which will be created the first time Jenkins is installed as C:\program files\jenkins\secrets\initialAdminPassword

    jenkins_jar_location: $env:TEMP/jenkins-cli.jar

The location at which the `jenkins-cli.jar` jarfile will be kept. This is used for communicating with Jenkins via the CLI.

    jenkins_plugins: []

List of Jenkins plugins to be installed automatically during provisioning. (_Note_: This feature is currently undergoing some changes due to the `jenkins-cli` authentication changes in Jenkins 2.0, and may not work as expected.)

    jenkins_connection_delay: 5
    jenkins_connection_retries: 60

Amount of time and number of times to wait when connecting to Jenkins after initial startup, to verify that Jenkins is running. Total time to wait = `delay` * `retries`, so by default this role will wait up to 300 seconds before timing out.

    jenkins_java_options: "-Djenkins.install.runSetupWizard=false"

Extra Java options for the Jenkins launch command configured in the init file can be set with the var `jenkins_java_options`. By default the option to disable the Jenkins 2.0 setup wizard is added.

    jenkins_init_changes:
      - option: "JENKINS_ARGS"
        value: "--prefix={{ jenkins_url_prefix }}"
      - option: "JENKINS_JAVA_OPTIONS"
        value: "{{ jenkins_java_options }}"

Changes made to the Jenkins init script; the default set of changes set the configured URL prefix and add in configured Java options for Jenkins' startup. You can add other option/value pairs if you need to set other options for the Jenkins init file.


## Example Playbook

    - hosts: ci-server
      vars:
        jenkins_hostname: jenkins.example.com
      roles:
        - sirdy.win_jenkins

## License

GNU

## Author Information

This role was inspired by the linux role created by geerlingguy. 
