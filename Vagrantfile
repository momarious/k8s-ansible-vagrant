# kubernetes-cluster/Vagrantfile
IMAGE_NAME = "ubuntu/jammy64"   # Ubuntu 22.04 LTS
MASTER_NAME = "master"
WORKER_NBR = 2
NODE_NETWORK_BASE = "192.168.56"
POD_NETWORK = "192.168.0.0/16" 

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    # RAM and CPU config
    config.vm.provider "virtualbox" do |v|
        v.memory = 4069
        v.cpus = 2
    end

    
    # Master node
    config.vm.define MASTER_NAME do |master|
        master.vm.box = IMAGE_NAME
        master.vm.hostname = MASTER_NAME
        master.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.10"
        master.vm.network "forwarded_port", guest: 6443, host: 6443


        # Provision with Ansible
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/playbook.yml"
            ansible.inventory_path = "ansible/inventory.ini"  # Specify the custom inventory file
            ansible.extra_vars = {
                node_type: "master",
                node_ip: "#{NODE_NETWORK_BASE}.10",
                pod_network: "#{POD_NETWORK}"
            }
        end
    end

    # Worker nodes
    (1..WORKER_NBR).each do |i|
        config.vm.define "worker-#{i}" do |worker|
            worker.vm.box = IMAGE_NAME
            worker.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.#{i + 10}"
            worker.vm.hostname = "worker-#{i}"

            # Provision with Ansible
            worker.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/playbook.yml"
                ansible.inventory_path = "ansible/inventory.ini"  # Specify the custom inventory file
                ansible.extra_vars = {
                    node_type: "worker",
                    node_ip: "#{NODE_NETWORK_BASE}.#{i + 10}"
                }
            end
        end
    end
end