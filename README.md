
# 🚀 Ansible Redis Cluster Deployment 🚀

Automate the deployment of a Redis cluster using Ansible! Deploy multiple instances on the same server with systemd and enjoy an interactive initialization prompt.

## Prerequisites

- Ansible installed on the machine from which you run the playbook.
- redis-tools package installed so Ansible can initialize the cluster
- Target servers with SSH access.
- Ensure that the necessary ports (e.g., 6379, 16379) are open on the target servers.

## Usage

1. **Clone this repository:**
   ```
   git clone https://github.com/SmartechOpenSource/ansible_redis-cluster.git
   cd ansible_redis-cluster/playbooks
2. **Update the inventory.ini and playbook.yml file:**

      we want 2 Redis servers on each instance
    ```
    playbook.yml
   
      vars: 
        - redis_instances_per_host: 2 


    inventory.ini
    Keep the Formatting as is and add details of your target instances.
      [redis_hosts]
      redis-1 ansible_host=192.168.1.2
      redis-2 ansible_host=192.168.1.3
    ```
4. **Run the playbook and wait for the cluster init confirmation**
   ```
   ansible-playbook -i inventory.ini playbook.yml
   ```
 5. wait for it to finish

  
       this is a sample of what you get at the and
   
       ```
    TASK [redis_cluster : Display Redis cluster initialization command]
    "msg": "i will use this command to init the cluster: redis-cli --cluster create 192.168.1.2:6379 192.168.1.2:6380 192.168.1.3:6379 192.168.1.3:6380 --cluster-replicas 1 delegate_to: 192.168.1.2:6379"

    TASK [redis_cluster : Confirm Initialization] 
    [redis_cluster : Confirm Initialization]
    Redis cluster configuration complete. Do you want to initialize the cluster now? (y/n):
