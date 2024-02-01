# Just a background what we intend to do in this Docker trial
1. Use Multipass to launch several nodes on same machine
2. Run Docker Swarm on top of them
3. Run Microservices using Docker swarm
4. Do trials for auto-scaling up and down

## 1. Use Multipass to launch several nodes on same machine
1. Visit [Multipass](https://multipass.run/install)
2. Choose the Linux Installation or OS of your choice
3. Run **sudo snap install multipass**
4. Check **multipass version**
5. Search **multipass find** to see if we have Docker under multipass umbrella available
6. Run **multipass launch docker --name node1**
7. Similarly, create 5 more nodes

## 2. Run Docker Swarm on top of them
1. Do **multipass info node1** and make the note of IPv4 addr
2. Goto node1 > run **multipass shell node1**
2. Now you are inside node1 > check **docker --version**
3. Inside node1 run > docker swarm init --advertise-addr <enter IPv4 addr in Step1>
4. Docker swarm would be initialized
5. Now, generate a swarm toker for other nodes to join using below cmd:
   **docker swarm join-token manager**
   You should get some txt as example below :
   **docker swarm join --token <token_id>**
6. Goto node2 and node3 and use the txt from Step 5 to make node2 and node3 join the node1 as manager
   It should show : node1 as leader and node2 and node3 as reachable
7. Go back to node 1 and generate worker token using below command:
   **docker swarm join-token worker**
   You should get some txt as example below :
   **docker swarm join --token <token_id>**
8. Goto node4 and node5 and use the txt from Step 7 to make node 4 and node5 josin as worker
9. Now, we have 3 manager nodes and 2 worker nodes

## 3. Run Microservices using Docker swarm
1. Goto node1 and create a service as below :
   **docker service create --name web -p 8080:8080 --replicas 3 nigelpoulton/gsd:web2023**
2. Run **docker service ls** and you should see 3 replicas running
3. Now, try hitting the <ip_address_of_any_node>:8080 and you see a static website


## 4. Do trials for auto-scaling up and down
### A. Imperative Way
1. Now, it's time to scale up the service and we can do it using below command from any manager node:
   **docker service scale web=10**
   And you see a total 10 services running in sometime.
2. Run **docker service ls** and find those which are running on node 4 or 5
   And goto that node 4 or 5, let us try to kill the service
3. Now, go back to node and run **docker service ps web** it should still show 10/10 replicas as the killed
   would be replaced by the new ones created automatically as docker swarm makes sure the total available replicas are 10

### B. Declarative Way
1. First let us clear the service running in the above way using below command:
   **docker service rm web**
2. Goto folder 'getting_started_with_docker' and run the below command:
   **docker image build -t nigelpoulton/gsd:swarm2023 .**
   It should create a image with name nigelpoulton/gsd:swarm2023
3. Let us deploy the container using compose.yml file:
   **docker stack deploy -c compose.yml counter**
4. Run **docker stack ls** to check if stacks are created
5. Run **docker stack services counter** to verify that 10 replicas are created
6. Now, try hitting the <ip_address_of_any_node>:5001 and you see a static website
7. To play around like scale up or down, just goto compose.yml and udpate
   **replicas: 10** part
