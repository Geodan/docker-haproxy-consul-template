# haproxy-consul_template
HAProxy with Consul Template (based on the offical Docker image).

Currently we only support the version based on Alpine. The services are run simultaneously using [Supervisor](http://supervisord.org). Supervisor currently runs as *root* user.

## Usage
In order to run HAProxy with Consul Template a working Consul agent must be available. Inside the container
we use the hostname *consul* and port 8500 to connect to the agent. You have to use the option ```--add-host```
to map the name *consul* to the IP address where Consul is running. **Note:** currently we don't support
Consul agents running on other ports than 8500.

The Consul Template can be mounted using a volume on the local disk. Consul Template expects the template to be
located at */usr/local/etc/haproxy.cfg.ctmpl*.

Use the following command to start the container:

```docker run -d -P --add-host=consul:10.0.0.11 -v /localdir/haproxy.cfg.ctmpl:/usr/local/etc/haproxy/haproxy.cfg.ctmpl:ro boonen/haproxy-consul_template```
