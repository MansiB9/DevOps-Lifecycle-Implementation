# DevOps Project - Implementing DevOps Lifecycle

## Implementing DevOps Lifecycle on Website using Ansible, Docker, Jenkins

### Project Description
**Project Name:** DevOps Lifecycle Implementation for XYZ Software

#### Objective:
To implement a complete DevOps lifecycle for XYZ Software, ensuring automated build, test, and deployment processes for their product available on GitHub. The goal is to streamline and enhance the efficiency of the software development and deployment pipeline.

### Key Features:
1. **Automated Software Installation:**
   - Using Ansible to install Jenkins, Docker, and other necessary software on target machines.
2. **Git Workflow Implementation:**
   - Establishing a Git branching strategy with master and develop branches.
3. **Continuous Integration and Continuous Deployment (CI/CD):**
   - Setting up Jenkins to automate builds, tests, and deployments based on branch commits.
4. **Containerization:**
   - Using Docker to containerize the application, ensuring consistency across environments.
5. **Jenkins Pipeline:**
   - Defining Jenkins jobs for building, testing, and deploying the application using a Docker container.

### Benefits:
- **Efficiency:** Automating the build, test, and deployment processes reduces manual intervention and speeds up the development lifecycle.
- **Consistency:** Containerization ensures that the application runs consistently across different environments.
- **Reliability:** Automated testing and deployment reduce the risk of human error and increase the reliability of releases.
- **Scalability:** The infrastructure and processes are scalable, allowing the company to grow without significant changes to the pipeline.

---

## Step 1: Launch Instances & Install Necessary Software
- Launch EC2 instances: **master, slave1, slave2**.
- Install necessary software like **Ansible** using the commands in `ansible-installation.sh`.
- Verify installation:
  ```sh
  ansible --version
  ```

### SSH Key Configuration:
1. Create SSH keys on the **Master** instance:
   ```sh
   ssh-keygen
   ```
2. Copy the public key:
   ```sh
   cd .ssh/
   cat id_rsa.pub
   ```
3. Paste the public key into the `authorized_keys` file on **Slave1** and **Slave2**:
   ```sh
   vi authorized_keys
   ```

### Configure Ansible Host File:
- Add **Slave IPs** in the Ansible host file:
  ```sh
  sudo nano /etc/ansible/hosts
  ```
  **Example:**
  ```ini
  slave1 ansible_host=168.31.29.124
  slave2 ansible_host=168.31.29.96
  ```
- Verify Ansible connectivity:
  ```sh
  ansible -m ping all
  ```

### Create Ansible Playbooks:
- Install Jenkins, Docker, and other dependencies:
  ```sh
  sudo nano ansible-playbook.yaml
  ```
- Create installation scripts:
  ```sh
  sudo nano master.sh
  sudo nano slave.sh
  ```
- Verify installations:
  ```sh
  docker --version
  jenkins --version
  java --version
  ```

---

## Step 2: Set Up Jenkins (CI/CD)
- Access Jenkins:
  ```sh
  http://<public-ip>:8080/
  ```
- Retrieve the Jenkins initial admin password:
  ```sh
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
- Configure Jenkins:
  - Install suggested plugins.
  - Create necessary credentials.
  - Add **Slave1** and **Slave2** as Jenkins nodes.

---

## Step 3: Implement Git Workflow
- **Branch Structure:**
  - `master` branch: Stable production code.
  - `develop` branch: Active development and feature integration.
- Clone the Git repository:
  ```sh
  git clone <repository-url>
  ```
- Push commits:
  ```sh
  git push --all
  ```
- Create a Webhook for triggering Jenkins jobs.

---

## Step 4: Containerization with Docker
- Create a `Dockerfile`:
  ```sh
  sudo nano Dockerfile
  ```
- Build and run the Docker container:
  ```sh
  sudo docker build . -t finalrelease
  sudo docker run -itd -p 80:80 finalrelease
  ```

---

## Step 5: Jenkins Pipeline Setup
### Define Jenkins Jobs:
1. **Job 1: Build**
2. **Job 2: Test**
3. **Job 3: Prod**

### Create a Test Job:
- In Jenkins:
  - Go to **New Item > Freestyle Project**.
  - Configure **Git Repository URL**.
  - Set **Branch Specifier** as `*/develop`.
  - Choose **GitHub hook trigger for GITScm polling**.
  - Click **Apply** and **Save**.

### Create a Prod Job:
- Modify **Branch Specifier** to `*/master`.
- Add Build Steps:
  ```sh
  sudo docker build . -t finalrelease
  sudo docker run -itd -p 80:80 finalrelease
  ```

---

## Final Steps:
- Modify the `index.html` file in GitHub.
- Trigger a Jenkins build using Webhook.
- Check the **console output** in Jenkins.
- Verify deployment by accessing the **public IP** of **Slave2**.

---

## Automation Summary:
✅ **Ansible** automates software installation.
✅ **Jenkins** enables CI/CD.
✅ **Docker** ensures consistent deployment.
✅ **GitHub** manages version control.
✅ **Jenkins Webhooks** trigger automated deployments.

🎯 **Final Output:** Successful implementation of a fully automated DevOps lifecycle!

![github3](https://github.com/user-attachments/assets/ce085332-0aa6-44ad-8bfd-62a148ae2dab)
