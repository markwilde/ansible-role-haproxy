# Ansible Role: HAProxy

A very basic ansible role for installing HAProxy on Ubuntu (only tested on 12.04).

## Example Configuration

```yaml
haproxy:
  global:
    log:
      - address: 127.0.0.1
        facility: local0
        level: notice
    maxconn: 2000
    user: haproxy
    group: haproxy
    daemon: true
  defaults:
    log: global
    mode: http
    timeouts:
      connect: 5000
      client: 10000
      server: 10000
    retries: 3
    options:
      - httplog
      - dontlognull
      - redispatch
  frontend: []
  backend: []
  listen:
    - name: stats
      bind: '*:80'
      mode: http
      stats:
        enable: true
        uri: /haproxy?stats
        realm: "Strictly Private"
        auth:
          - user: admin
            pass: password
      balance: roundrobin
      options:
        - httpclose
        - forwardfor
      servers: []
```

## TODO
Add support for frontend and backend