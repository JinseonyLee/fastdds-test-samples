
## Discovery Server setting

```bash
ddsrouter -c dds-router-ds.yaml 
```


## Talker Setting

```bash
cd dds-router/talker
docker build -t ddsrouter-talker . 
```

```bash
docker run -it  --name talker --network host ddsrouter-talker:latest ros2 run demo_nodes_cpp talker 
```


## Listener Setting

```bash
cd dds-router/listener
docker build -t ddsrouter-listener . 
```

```bash
docker run -it  --name listener --network host ddsrouter-listener:latest ros2 run demo_nodes_cpp listener 
```

