
## Discovery Server setting

```bash
#ddsrouter -c dds-router-ds.yaml 
export FASTRTPS_DEFAULT_PROFILES_FILE="/home/ubuntu/fastdds-test-samples/dds-router-over-tcp/fastdds-ds.xml"
export RMW_IMPLEMENTATION="rmw_fastrtps_cpp"

fastdds discovery -i 0 -x fastdds-ds.xml 
```


## Talker Setting

```bash
cd dds-router-over-tcp/talker
docker build -t tcp-talker .
```

```bash
docker run -it  --name tcp-talker --network host tcp-talker:latest ros2 run demo_nodes_cpp talker 
```

```bash
docker run -it  --name ddsrouter-tcp-talker --network host ddsrouter-tcp-talker:latest ros2 run demo_nodes_cpp talker 
```
docker run -it  --name ddsrouter-tcp-talker  -p 49154:49154 -p 49155:49155 ddsrouter-tcp-talker:latest ros2 run demo_nodes_cpp talker 

## Listener Setting

```bash
cd dds-router-over-tcp/listener
docker build -t tcp-listener .
```

```bash
docker run -it  --name listener --network host tcp-listener:latest ros2 run demo_nodes_cpp listener 
```

```bash
docker run -it  --name ddsrouter-tcp-listener --network host ddsrouter-tcp-listener:latest ros2 run demo_nodes_cpp listener 
```
docker run -it  --name ddsrouter-tcp-listener  -p 49153:49153 -p 49152:49152 ddsrouter-tcp-listener:latest ros2 run demo_nodes_cpp listener 