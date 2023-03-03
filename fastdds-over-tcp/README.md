
## Discovery Server setting

```bash
export FASTRTPS_DEFAULT_PROFILES_FILE="/home/ubuntu/fastdds-test-samples/dds-router-only-over-tcp/fastdds-ds.xml"
export RMW_IMPLEMENTATION="rmw_fastrtps_cpp"

fastdds discovery -i 0 -x fastdds-ds.xml 
```


## Talker Setting

```bash
cd dds-router-over-tcp/talker
docker build -t tcp-talker .
```

```bash
docker run -it  --name tcp-talker  -p 49154:49154 tcp-talker:latest ros2 run demo_nodes_cpp talker 
```

## Listener Setting

```bash
cd dds-router-over-tcp/listener
docker build -t tcp-listener .
```

```bash
docker run -it  --name tcp-listener -p 49152:49152 tcp-listener:latest ros2 run demo_nodes_cpp listener 
```
