# sawtooth-physical-multinode
sawtooth network with docker swarm to enable physical multi node setup
Setting up Docker Swarm involves creating a cluster of Docker hosts and orchestrating container deployments across them. Here's a basic guide on setting up Docker Swarm:

### Prerequisites:
1. **Docker Installed:**
   - Make sure Docker is installed on all the machines that will be part of the Swarm.

2. **Networking:**
   - Ensure that all nodes can communicate with each other over the network.

### Steps to Set Up Docker Swarm:

#### Step 1: Initialize the Swarm on Manager Node
On the machine that you want to designate as the manager node, open a terminal and run the following command:

```bash
docker swarm init --advertise-addr <MANAGER-IP>
```

Replace `<MANAGER-IP>` with the actual IP address of the manager node. This command initializes the Swarm and provides you with a token for joining worker nodes.

#### Step 2: Join Worker Nodes
On each machine that you want to join as a worker node, run the command obtained from the previous step. It will look something like this:

```bash
docker swarm join --token <TOKEN> <MANAGER-IP>:<MANAGER-PORT>
```

Replace `<TOKEN>`, `<MANAGER-IP>`, and `<MANAGER-PORT>` with the actual token and manager node details provided by the `docker swarm init` command.

#### Step 3: Verify Swarm Status
Back on the manager node, run the following command to verify that all nodes have successfully joined the Swarm:

```bash
docker node ls
```

This should display a list of nodes with their status.

#### Step 4: Deploy Services
Now that your Swarm is set up, you can deploy services across the nodes. Create a Docker Compose file (e.g., `docker-compose.yml`) specifying your services and deploy them using:

```bash
docker stack deploy -c docker-compose.yml <STACK-NAME>
```

Replace `<STACK-NAME>` with a suitable name for your stack.

#### Step 5: Scale Services
You can scale your services by adjusting the number of replicas. For example:

```bash
docker service scale <SERVICE-NAME>=<NUMBER-OF-REPLICAS>
```

Replace `<SERVICE-NAME>` and `<NUMBER-OF-REPLICAS>` with your service name and the desired number of replicas.

### Additional Tips:
- Use Docker Compose for defining multi-container applications.
- Use Swarm Visualizer or Portainer for a graphical representation of your Swarm.

Keep in mind that this is a basic setup. Depending on your needs, you might want to configure security, networking, and other aspects of your Swarm. Refer to the official Docker documentation for more details: [Docker Swarm Mode](https://docs.docker.com/engine/swarm/).
