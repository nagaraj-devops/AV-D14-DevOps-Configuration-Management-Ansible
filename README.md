# AV-D14-DevOps-Configuration-Management-Ansible
AV-D14-DevOps-Configuration-Management-Ansible

# DevOps – Configuration Management with Ansible

## 🔹 What is Configuration Management?
Configuration Management (CM) is the practice of **automating the setup, configuration, and maintenance** of systems and applications to ensure consistency across environments (Dev, QA, Prod).  

- Ensures **consistency** in server states  
- Reduces **manual effort & human errors**  
- Provides **scalability** for managing thousands of servers  
- Enables **auditability & version control** of infrastructure  

## 🔹 Why Ansible?
- **Agentless** → No need to install agents on target machines (uses SSH/WinRM).  
- **Simple** → YAML-based playbooks (human-readable).  
- **Idempotent** → Running the same playbook multiple times ensures same state.  
- **Extensible** → Supports plugins, modules, roles, and collections.  
- **Integration** → Works with CI/CD pipelines (Jenkins, GitLab, GitHub Actions).  

## 🔹 Ansible Architecture
1. **Control Node**
   - Where Ansible is installed and commands are run.  
   - Executes playbooks on target nodes.  

2. **Inventory**
   - List of target hosts (static or dynamic).  
   - Example: `hosts.ini`
     ```ini
     [webservers]
     server1 ansible_host=192.168.1.10
     server2 ansible_host=192.168.1.11
     ```

3. **Playbooks**
   - Written in **YAML** to define desired states.  
   - Example:
     ```yaml
     - hosts: webservers
       become: yes
       tasks:
         - name: Install Apache
           apt:
             name: apache2
             state: present
     ```

4. **Modules**
   - Pre-built scripts to manage services, packages, files, etc.  
   - Example: `apt`, `yum`, `copy`, `service`, `user`.  

5. **Roles**
   - Structured way to organize playbooks (tasks, handlers, vars, templates, defaults).  

6. **Handlers**
   - Triggered when a task changes something.  
   - Example: Restarting a service if a config file changes.  

## 🔹 Common Ansible Commands
- **Run ad-hoc command**  
  ```bash
  ansible all -i hosts.ini -m ping
  ```
- **Run a playbook**  
  ```bash
  ansible-playbook -i hosts.ini site.yml
  ```
- **Check mode (dry run)**  
  ```bash
  ansible-playbook -i hosts.ini site.yml --check
  ```
- **Limit execution to a host**  
  ```bash
  ansible-playbook site.yml --limit server1
  ```

## 🔹 Use Cases
- Provisioning new servers  
- Installing & configuring applications  
- Deploying updates  
- Security patching  
- Continuous Delivery pipelines  
- Cloud infrastructure automation (AWS, Azure, GCP)  

## 🔹 Example: Install & Start Nginx
```yaml
- hosts: webservers
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Ensure Nginx is running
      service:
        name: nginx
        state: started
        enabled: yes
```

## 🔹 Benefits of Ansible in DevOps
- **Consistency** across environments  
- **Faster deployments**  
- **Easy rollback** via playbook re-runs  
- **Scalability** → manage thousands of servers  
- **Integration** → GitOps, Jenkins, Kubernetes
