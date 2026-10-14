# Experiment 6: Exploration of Cloud Service Models (IaaS, PaaS, SaaS) Using a Free-Tier Cloud Platform

## 1. Aim

To explore the three cloud service models (IaaS, PaaS, SaaS) by using services on a free-tier cloud platform and to compare their responsibilities, control, and use cases.

## 2. Objectives

- Understand cloud computing characteristics and service models.
- Provision an IaaS resource (virtual machine).
- Deploy an application on a PaaS service.
- Use a SaaS application and compare the level of user control.
- Understand cost control and clean-up practices.

## 3. Requirements

| Item | Details |
|---|---|
| Cloud account | One of: AWS Free Tier, Microsoft Azure free account, Google Cloud free tier (any works; the steps give examples for each) |
| Other | Email address, a verified payment card (usually required for sign-up), web browser, SSH client (Terminal, PuTTY, or the cloud's browser SSH) |

> **Cost warning:** Free-tier terms (duration, limits, eligible services) change. Read the current terms on the provider's site, set a **budget alert**, and **delete all resources at the end** of the experiment to avoid charges.

## 4. Theory

### 4.1 Cloud Characteristics

On-demand self-service, broad network access, resource pooling, rapid elasticity, and measured service.

### 4.2 Service Models

| Model | You Manage | Provider Manages | Example Services | Typical Users |
|---|---|---|---|---|
| **IaaS** (Infrastructure as a Service) | OS, middleware, runtime, applications, data | Virtualization, servers, storage, networking | AWS EC2, Azure Virtual Machines, Google Compute Engine | System administrators, DevOps |
| **PaaS** (Platform as a Service) | Applications and data | Everything below the application (OS, runtime, scaling) | AWS Elastic Beanstalk, Azure App Service, Google App Engine, Heroku | Developers |
| **SaaS** (Software as a Service) | Only your usage and configuration | The entire application stack | Gmail, Microsoft 365, Zoho, Salesforce | End users |

### 4.3 Shared Responsibility Overview

```
            On-premises      IaaS        PaaS        SaaS
Application   You            You         You         Provider
Data          You            You         You         You (config/data)
Runtime       You            You         Provider    Provider
OS            You            You         Provider    Provider
Virtualization You           Provider    Provider    Provider
Hardware      You            Provider    Provider    Provider
```

### 4.4 Deployment Models

Public, private, hybrid, and community clouds.

## 5. Procedure

### Part A: Account Setup and Cost Safety

1. Sign up for a free-tier account with your chosen provider.
2. Enable multi-factor authentication on the root/owner account.
3. Create a **budget alert** (for example, notify at a very low amount):
   - AWS: Billing > Budgets
   - Azure: Cost Management > Budgets
   - Google Cloud: Billing > Budgets & alerts
4. Note the free-tier limits that apply to the services you will use.

### Part B: IaaS: Launch a Virtual Machine

**AWS example (EC2)**

1. Open the **EC2** console and select **Launch instance**.
2. Name the instance, choose a **free-tier eligible** Linux image (e.g., Amazon Linux or Ubuntu) and a free-tier eligible instance type (e.g., t2.micro or t3.micro, as shown in the console).
3. Create a key pair and download the `.pem` file.
4. In network settings, allow SSH (port 22) from **your IP only**, and HTTP (port 80).
5. Launch the instance and wait for **running** status.
6. Connect with SSH:

```bash
chmod 400 mykey.pem
ssh -i mykey.pem ec2-user@<PUBLIC_IP>
```

7. Install a web server and publish a page (Ubuntu example):

```bash
sudo apt update
sudo apt install -y nginx
echo "<h1>Hello from IaaS</h1>" | sudo tee /var/www/html/index.html
```

8. Open `http://<PUBLIC_IP>` in a browser and confirm the page loads.
9. Note what **you** had to do: choose OS, patch it, install software, configure firewall.

*Equivalents:* Azure > Virtual Machines > Create; Google Cloud > Compute Engine > Create instance.

### Part C: PaaS: Deploy a Web Application

Use a simple sample app (for example, a small Flask app).

`app.py`:

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from PaaS"

if __name__ == "__main__":
    app.run()
```

`requirements.txt`:

```
flask
gunicorn
```

**Option 1: AWS Elastic Beanstalk**

1. Zip `app.py` and `requirements.txt` (rename the entry module/object as Beanstalk expects, e.g., `application.py` with `application = Flask(__name__)`, or set a Procfile: `web: gunicorn app:app`).
2. Open Elastic Beanstalk > Create application > Web server environment, platform **Python**, upload the zip.
3. Wait for the environment to become healthy, then open the provided URL.

**Option 2: Azure App Service**

1. Create a Web App, runtime **Python**, free (F1) or lowest tier.
2. Deploy using ZIP deploy or GitHub integration.

**Option 3: Google App Engine**

1. Add an `app.yaml` with `runtime: python312` (or the currently supported version).
2. Deploy with `gcloud app deploy`.

Note what **the provider** handled: OS patching, runtime installation, load balancing, scaling configuration.

### Part D: SaaS: Use a Ready-Made Application

1. Use a SaaS application (e.g., Gmail, Google Docs/Sheets, Microsoft 365 web apps, or Zoho).
2. Perform a simple task: create a shared document or spreadsheet, invite a collaborator, and review sharing permissions.
3. Note that you installed, patched, and scaled nothing.

### Part E: Observe Elasticity and Monitoring (Optional)

1. Open the provider's monitoring service (CloudWatch, Azure Monitor, Cloud Monitoring).
2. View CPU utilization of your VM or app.
3. Review the scaling or auto-scaling options available for the PaaS service.

### Part F: Clean Up (Mandatory)

1. Terminate/delete the VM, associated disks, and public IP addresses.
2. Delete the PaaS environment/app and any storage buckets created.
3. Check the billing dashboard to confirm no active resources remain.

## 6. Observations

### Service Comparison

| Aspect | IaaS (VM) | PaaS (App Service) | SaaS (App) |
|---|---|---|---|
| Service used | | | |
| Setup time | | | |
| OS access | | | |
| Software installation needed | | | |
| Scaling effort | | | |
| Customization possible | | | |
| Maintenance by you | | | |

### Resource Record

| Resource | Provider | Region | Created | Deleted |
|---|---|---|---|---|
| | | | | |

## 7. Result

IaaS, PaaS, and SaaS were explored on a free-tier cloud platform, and the differences in control, responsibility, and effort were observed.

## 8. Conclusion

IaaS offers maximum control with maximum responsibility, PaaS lets developers focus on code, and SaaS provides ready-to-use software with minimal management. The right choice depends on control needs, skills, and speed of delivery. Good cost hygiene (budgets, clean-up) is essential in the cloud.

## 9. Viva Questions

1. Define cloud computing and list its essential characteristics.
2. Differentiate IaaS, PaaS, and SaaS with examples.
3. Which model gives the most control over the operating system?
4. What is the shared responsibility model?
5. What is elasticity and how does it differ from scalability?
6. Where does a no-code platform such as Zoho Creator fit among these models?
