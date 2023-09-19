# Ansible Role: Tomcat 9

An Ansible Role that installs Tomcat 9.0 or 10.0 on Debian/Ubuntu.

## Role Variables

### tomcat packages state; use `present` to make sure it's installed

tomcat_packages_state: present

Available variables are listed below, along with default values (see `defaults/main.yml`):

tomcat_server_root: /etc/{{ tomcat_service }}

The server root for config files (tomcat_service) normally tomcat9 or tomcat10.

    tomcat_run_user: "tomcat"
    tomcat_run_group: "tomcat"

Default user and group where tomcat run as.

    tomcat_server_logs_directory: "logs"
    tomcat_server_logs_rotatable: "true"
    tomcat_server_logs_prefix: "localhost_access_log"
    tomcat_server_logs_suffix: ".txt"
    tomcat_server_logs_pattern: "%h %l %u %t &quot;%r&quot; %s %b"
    tomcat_logging_properties_handlers: "1catalina.org.apache.juli.AsyncFileHandler, 2localhost.org.apache.juli.AsyncFileHandler, java.util.logging.ConsoleHandler"

Default configs for logging options.

    tomcat_catalina_properties_common_loader: '"${catalina.base}/lib","${catalina.base}/lib/*.jar","${catalina.home}/lib","${catalina.home}/lib/*.jar"'

Default catalina config properties in common loader section.

    tomcat_server_connector: '<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />'

Default tomcat server connector.

    tomcat_server_engine: '<Engine name="Catalina" defaultHost="localhost">'

Default tomcat server engine.

    tomcat_server_valve_addons:
    tomcat_context_xml_addons:
    tomcat_logging_properties_handlers_addons:

Especial configs for server, context and logging if you like.

    tomcat_enabled: yes

Set the tomcat service boot time status. This should generally remain `yes`, but you can set it to `no` if you need to run Ansible while leaving the service disabled.

## Dependencies

None.

## Example Playbook

    - hosts: webservers
      vars_files:
        - vars/main.yml
      roles:
        - { role: socket.tomcat }

## License

MIT / BSD

## Author Information

This role was created in 2023 by [Juan Carlos Giménez Moncada](https://www.opensocket.es/).
