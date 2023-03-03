
## Discovery Server setting

```bash
export FASTRTPS_DEFAULT_PROFILES_FILE="/home/ubuntu/fastdds-test-samples/dds-router-only-over-tcp/fastdds-ds.xml"
export RMW_IMPLEMENTATION="rmw_fastrtps_cpp"

ddsrouter -c ddsrouter-discoveryserver.yaml
```


## Talker Setting

```bash
cd dds-router-over-tcp/talker
docker build -t ddsrouter-tcp-talker .
```

```bash
docker run -it  --name ddsrouter-tcp-talker  -p 49154:49154 ddsrouter-tcp-talker:latest ros2 run demo_nodes_cpp talker 
```

## Listener Setting

```bash
cd dds-router-over-tcp/listener
docker build -t ddsrouter-tcp-listener .
```

```bash
docker run -it  --name ddsrouter-tcp-listener -p 49152:49152 ddsrouter-tcp-listener:latest ros2 run demo_nodes_cpp listener 
```
