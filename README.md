# Auto-Healing Web Tier (AWS + Terraform)

This repository demonstrates how to deploy an auto-healing, load-balanced web tier on AWS using Terraform and Docker. The solution uses modular Terraform code and a Docker container to serve a static NGINX "welcome" page.

---

### Requirements
1. **Tools:**
   - Terraform v1.x
   - AWS CLI
   - Docker (for building/pushing the custom image)
2. **AWS:**
   - An AWS account
   - Access keys configured locally

---

### Running the Code
1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd auto-healing-web-tier
   ```

2. Build and push the Docker image:
   ```bash
   docker build -t <your-dockerhub-username>/nginx-welcome:latest .
   docker push <your-dockerhub-username>/nginx-welcome:latest
   ```

3. Initialize Terraform:
   ```bash
   terraform init
   ```

4. Apply the Terraform configuration **(plan first)**:
   ```bash
   terraform plan -out=tfplan
   terraform apply tfplan
   ```

5. Access the load balancer DNS:
   - Terraform output will include the ALB's DNS name. Open it in your browser to view the NGINX welcome page.

---

### Architecture
![Auto-healing Web Tier Architecture](diagrams/architecture.png)

---

### Assumptions
- AWS free tier is used where possible.
- Instances are lightweight (t3.micro) and designed for testing/development, minimizing costs.

---

### Estimated Monthly Cost
| Component                 | Details                  | Approx AUD |
|---------------------------|--------------------------|------------|
| Load Balancer (ALB)       | 750 hours/month          | 15.00      |
| EC2 Instances (2x t3.micro) | 750 hours x 2          | 2.30       |
| Total                     |                          | **17.30**  |

This assumes the use of AWS Pricing Calculator and free-tier allowances.

---

### Pipeline
This repository includes an optional CI pipeline (`pipeline.yml`) for validating the Terraform code.

---

### Pending Improvements
- Add unit testing for Dockerfile.
- Expand support for Azure with Bicep.

---

### Acknowledgments
This project uses AWS and Terraform best practices for deploying reliable, self-healing systems.
