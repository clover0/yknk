# yknk. Simple and easy task execution tool


1. Write YAML file.
1. Run `yknt` command, with YAML file.

#### yknk...
yknk is from 'Yakiniku'.

# Example
For network simple checker.

### YAML
```yaml
version: 1
flow:
  name: "example.com"
  concurrent: true
  tasks:
    - name: "Application and check IP"
      concurrent: true
      tasks:
        - name: "Get example.com"
          command: curl
          args: [ "--head", "-sS","https://example.com" ]
        - name: "Reach packet"
          command: ping
          args: [ "-c","3","example.com" ]
    - name: "Port"
      concurrent: false
      tasks:
        - name: "Connect 80"
          command: nc
          args: [ "example.com","80"]
        - name: "Connect 8080"
          command: nc
          args: [ "example.com","8080"]
```

### Result
```
==============================
name: Application and check IP
exec:  []
    name: Get example.com
    exec: curl [--head -sS https://example.com]
    name: Reach packet
    exec: ping [-c 3 example.com]
name: Port
exec:  []
    name: Connect 80
    exec: nc [example.com 80]
    name: Connect 8080
    exec: nc [example.com 8080]
     => Fail:(timeout)
==============================
Total: 6    Success: 5    Error: 1
```