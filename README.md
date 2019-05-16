![](https://img.shields.io/badge/Ansible-NGinx-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_nginx.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [NGinx Versions](#NGinx-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs NGinx on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `ngx_conf_path`: Specify the NGinx configure directory.
* `ngx_selinux`: SELinux security policy.
* `ngx_site_path`: Specify the NGinx site directory.
* `ngx_temp_path`: Defines a directory for storing temporary files.
* `ngx_version`: extras or standard, extras includes party modules likes PageSpeed,Brotli,ModSecurity,Headers-More and much more.

##### Log Variables
* `ngx_acc_syslog_port`: Defines the input port of a syslog server for access log.
* `ngx_err_syslog_port`: Defines the input port of a syslog server for error log.
* `ngx_logs_path`: Specify the NGinx logs directory.
* `ngx_syslog`: Enables or disables syslog.
* `ngx_syslog_server`: Defines the address of a syslog server.

##### Service Mesh
* `environments`: Define the service environment.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

##### Listen port
* `ngx_port_api`: Status listen port.
* `ngx_port_exporter`: NGinx exporter listen port.
* `ngx_port_http`: HTTP listen port.
* `ngx_port_https`: HTTPs listen port.

##### Customer Header Variables
* `ngx_header`: Adds the specified field to a response header

##### System Variables
* `ngx_arg.charset`: Adds the specified charset for response header field.
* `ngx_arg.client_body_timeout`: Defines a timeout for reading client request body.
* `ngx_arg.client_max_body_size`: The maximum allowed size of the client request body.
* `ngx_arg.etag`: Enables or disables the "ETag" response header field for static resources.
* `ngx_arg.expires`: Cache-Control response header fields.
* `ngx_arg.fastcgi_read_timeout`: Defines a timeout for reading a response from the FastCGI server.
* `ngx_arg.keepalive_requests`: The maximum number of requests that can be served through one keep-alive connection.
* `ngx_arg.keepalive_timeout`: Sets a timeout during which a keep-alive client connection will stay open on the server side.
* `ngx_arg.proxy_connect_timeout`: Defines a timeout for establishing a connection with a proxied server.
* `ngx_arg.proxy_read_timeout`: Defines a timeout for reading a response from the proxied server.
* `ngx_arg.proxy_send_timeout`: Sets a timeout for transmitting a request to the proxied server.
* `ngx_arg.real_ip_header`: Defines the request header field whose value will be used to replace the client address.
* `ngx_arg.send_timeout`: Sets a timeout for transmitting a response to the client.
* `ngx_arg.server_tokens`: Enables or disables nginx version on "Server" response header field.
* `ngx_arg.tcp_nodelay`: Enables or disables the use of the TCP_NODELAY option.
* `ngx_arg.tcp_nopush`: Enables or disables the use of the TCP_NOPUSH socket option.
* `ngx_arg.ulimit_nofile`: The number of files launched by systemd.
* `ngx_arg.ulimit_nproc`: The number of processes launched by systemd.
* `ngx_arg.user`: Defines user and group credentials used by worker processes.
* `ngx_arg.worker_connections`: The maximum number of simultaneous connections that can be opened by a worker process.
* `ngx_arg.worker_cpu_affinity`: Binds worker processes to the sets of processor.
* `ngx_arg.worker_processes`: Defines the number of worker processes.

##### Allow-Methods Variables
* `ngx_allow_methods`: # Define allowable HTTP methods.

##### DNS Variables
* `ngx_resolver_dns`: Configures name servers used to resolve names of upstream servers into addresses.
* `ngx_resolver_timeout`: Sets a timeout for name resolution.

##### Internal network segment
* `ngx_set_real_ip_from`: Defines trusted addresses that are known to send correct replacement addresses.

##### Security Variables
* `ngx_block_agents`: Enables or disables block unsafe User Agents.
* `ngx_block_string`: Enables or disables block includes Exploits / File injections / Spam / SQL injections.
* `ngx_modsecurity`: Enables or disables ModSecurity modules.
* `ngx_ssl_protocols`: intermediate or modern, defines SSL protocol profile.

##### Performance Variables
* `ngx_compress`: Enables or disables compression.
* `ngx_pagespeed`: Enables or disables pagespeed modules.

##### DH parameters
* `ngx_dhparam`: Enables or disables Diffie Hellman parameters.
* `ngx_dhparam_file`: Diffie Hellman key file.
* `ngx_dhparam_size`: Diffie Hellman key size.
* `ngx_dhparam_update`: Enables or disables key automatic updates.
* `ngx_dhparam_update_interval`: Key renewal period.

##### HTTP Public Key Pinning Extension
* `ngx_HPKP`: Public Key Pinning.


##### Business Topology
* `ngx_site`: Define backend traffic context.

### Other parameters
There are some variables in vars/main.yml:

* `ngx_kernel_parameters`: Operating system variables.
* `ngx_conf_scripts`: Specify the MongoDB configure and script files.

## Dependencies
There are no dependencies on other roles.

## Example
### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-nginx
           ngx_version: 'standard'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    ngx_conf_path: '/etc/nginx'
    ngx_selinux: false
    ngx_site_path: '/data/nginx_site'
    ngx_temp_path: '/dev/shm'
    ngx_version: 'standard'
    ngx_acc_syslog_port: '12301'
    ngx_err_syslog_port: '12302'
    ngx_logs_path: '/data/nginx_logs'
    ngx_syslog: false
    ngx_syslog_server: '1.1.1.1'
    ngx_port_api: '10088'
    ngx_port_exporter: '9113'
    ngx_port_http: '80'
    ngx_port_https: '443'
    ngx_header:
      - 'Referrer-Policy "no-referrer-when-downgrade";'
      - 'Strict-Transport-Security "max-age=31536000; includeSubDomains; preload;";'
      - 'X-Content-Type-Options "nosniff";'
      - 'X-Frame-Options "SAMEORIGIN";'
      - 'X-Xss-Protection "1; mode=block";'
    ngx_arg:
      charset: 'utf-8'
      client_body_timeout: '10'
      client_max_body_size: '2m'
      etag: 'off'
      expires: 'max'
      fastcgi_read_timeout: '60'
      keepalive_requests: '5000'
      keepalive_timeout: '15'
      proxy_connect_timeout: '20'
      proxy_read_timeout: '20'
      proxy_send_timeout: '20'
      real_ip_header: 'X-Forwarded-For'
      send_timeout: '30'
      server_tokens: 'off'
      tcp_nodelay: 'on'
      tcp_nopush: 'on'
      ulimit_nofile: '131088'
      ulimit_nproc: '131088'
      user: 'nobody'
      worker_connections: '20480'
      worker_cpu_affinity: 'auto'
      worker_processes: 'auto'
    ngx_allow_methods:
      - 'POST'
      - 'PUT'
      - 'GET'
      - 'HEAD'
    ngx_resolver_dns:
      - '223.5.5.5'
      - '223.6.6.6'
      - '8.8.8.8'
    ngx_resolver_timeout: '5s'
    ngx_set_real_ip_from:
      - '10.0.0.0/8'
      - '172.16.0.0/11'
      - '192.168.0.0/24'
      - '127.0.0.1'
    ngx_block_agents: false
    ngx_block_string: false
    ngx_modsecurity: false
    ngx_ssl_protocols: 'modern'
    ngx_compress: false
    ngx_pagespeed: false
    ngx_dhparam: false
    ngx_dhparam_file: 'dhparam.pem'
    ngx_dhparam_size: '2048'
    ngx_dhparam_update: true
    ngx_dhparam_update_interval: 'monthly'
    ngx_HPKP:
      - 'bb+uANN7nNc/j7R95lkXrwDg3d9C286sIMF8AnXuIJU='
      - 'du6FkDdMcVQ3u8prumAo6t3i3G27uMP2EOhR8R0at/U='
      - '980Ionqp3wkYtN9SZVgMzuWQzJta1nfxNPwTem1X0uc='
    ngx_site:
      - domain: 'a.example.com'
        type: 'proxy'
        location: '/'
        syntax:
          - 'expires -1'
          - 'proxy_set_header Host $http_host'
        backend_address:
          - '1.1.1.1'
          - '1.1.1.2'
        backend_port: '8080'
        sticky: 'ip_hash'
        keepalive: '32'
    environments: 'SIT'
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_clients: 'localhost'
    consul_public_http_port: '8500'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
