# Ansible Concurrency and Parallelism

This repository contains code materials and examples for the article "[เขียน Ansible Playbook ยังไงให้ทำงานได้เร็วขึ้น?](https://nopnithi.com/posts/how-to-write-ansible-playbooks-to-make-it-run-faster/)" (How to Write Ansible Playbooks to Make It Run Faster?). The article explains various techniques to improve the performance and speed of Ansible playbooks by leveraging concurrency and parallelism.

## Prerequisites

To follow along with the hands-on examples in this repository, make sure you have the following prerequisites installed:

1. Python 3 (the article uses version 3.12.3)
2. Ansible (the article uses version 2.16.5)
3. sshpass (the article uses version 1.10)
4. Docker (the article uses version 26.0.0, build 2ae903e)
5. Git (the article uses version 2.44.0)

## Getting Started

To get started with the code examples, follow these steps:

1. Clone this repository:
   ```
   git clone https://github.com/nopnithi/ansible-concurrency-and-parallelism.git
   ```

2. Build the Docker image:
   ```
   docker build -t ansible-managed-node .
   ```

3. Run the Docker containers to simulate managed nodes:
   ```
   docker run -d --name node01-windows -p 2201:22 ansible-managed-node
   docker run -d --name node02-debian -p 2202:22 ansible-managed-node
   docker run -d --name node03-ubuntu -p 2203:22 ansible-managed-node
   docker run -d --name node04-centos -p 2204:22 ansible-managed-node
   docker run -d --name node05-windows -p 2205:22 ansible-managed-node
   docker run -d --name node06-debian -p 2206:22 ansible-managed-node
   docker run -d --name node07-ubuntu -p 2207:22 ansible-managed-node
   docker run -d --name node08-centos -p 2208:22 ansible-managed-node
   ```

4. Test the connectivity to the managed nodes using Ansible's `ping` module:
   ```
   ansible all -i hosts -m ping
   ```

## Repository Structure

The repository has the following structure:

```
.
├── Dockerfile
├── README.md
├── ansible.cfg
├── hosts
└── playbooks
    ├── 01_forks.yaml
    ├── 02_serial1.yaml
    ├── 03_serial2.yaml
    ├── 04_serial3.yaml
    ├── 05_linear_strategy.yaml
    ├── 06_free_strategy.yaml
    ├── 07_synchronous.yaml
    ├── 08_asynchronous1.yaml
    └── 09_asynchronous2.yaml
```

- `Dockerfile`: Contains the configuration for building the Docker image used as the managed nodes.
- `ansible.cfg`: Ansible configuration file used in the examples.
- `hosts`: Inventory file defining the managed nodes and their variables.
- `playbooks/`: Directory containing various Ansible playbooks demonstrating different techniques for concurrency and parallelism.

## Techniques Covered

The article and the code examples in this repository cover the following techniques for improving Ansible playbook performance:

1. Using `forks` to control the number of nodes running in parallel.
2. Utilizing `serial` to divide nodes into batches and reduce risks associated with running tasks on a large number of nodes simultaneously.
3. Choosing between `linear` (default) and `free` strategies to speed up playbook execution when tasks are not required to run on certain nodes.
4. Employing `async` for long-running tasks to allow other tasks to run while waiting for the asynchronous tasks to complete.

Please refer to the [article](https://nopnithi.com/posts/how-to-write-ansible-playbooks-to-make-it-run-faster/) for detailed explanations and insights on each technique.

## Conclusion

By exploring and applying the techniques demonstrated in this repository, you can significantly improve the performance and speed of your Ansible playbooks. However, keep in mind that each technique has its own advantages and disadvantages, and you should consider them based on your specific use case and requirements.

Feel free to explore the code examples, experiment with different configurations, and adapt them to suit your needs. If you have any questions or suggestions, please don't hesitate to reach out.
