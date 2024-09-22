# Swarm notes

creation

```bash
# swarm-1
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl start docker
sudo systemctl enable docker

# Init new swarm
docker swarm init --advertise-addr 192.168.1.90
mkdir /data
mkdir /data/b2share
```

```bash
# swarm-2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl start docker
sudo systemctl enable docker

# Join the swarm
docker swarm join --token SWMTKN-1-5lh0jarrcqnqgik9l30567ccv51jv2n3zwnmfgisv8zu89yfxu-8hwrt3ybf1ueb17zgwphlerxy 192.168.1.90:2377
```

Configure remote access with systemd: https://docs.docker.com/engine/daemon/remote-access/

from local machine:
```bash
ssh -L 2375:localhost:2375 almalinux@86.50.228.13
export DOCKER_HOST='tcp://localhost:2375'
docker node ls
```

Separated docker-compose file to two. General services to be used with every deployment and application specific. Modified docker compose general file to put all services to node 1, except nginx, that goes to all machines, thus possible to dns to all instances and redirect to correct container.

Added `ulimit -n 1024` to elasticsearch Dockerfile

```bash
docker stack deploy -c docker-compose-general.yml b2share1
```
