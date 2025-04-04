# Photo Sharing Website - CI/CD with Jenkins & Docker

This project is a simple photo-sharing website deployed using Jenkins and Docker. The CI/CD pipeline automates building, testing, and deploying the application.

## **Project Overview**
- **Frontend:** Static website (HTML, CSS, JavaScript)
- **Backend:** Nginx (serving static files)
- **Deployment:** Dockerized and hosted on an EC2 instance
- **CI/CD Tool:** Jenkins

## **CI/CD Workflow**

### **1. Jenkins Pipeline Steps**
1. **Pull latest code** from GitHub repository.
2. **Remove old container** running on port `8081` (if any).
3. **Remove old Docker image** to ensure a clean build.
4. **Build a new Docker image** using the latest code.
5. **Run a new container** on port `8081`.

### **2. Jenkins Freestyle Job Configuration**
1. **Source Code Management:** GitHub repository
2. **Build Steps (Execute Shell):**
   ```sh
   # Stop and remove existing container on port 8081
   sudo docker ps -q --filter "publish=8081" | xargs -r sudo docker stop
   sudo docker ps -aq --filter "publish=8081" | xargs -r sudo docker rm

   # Remove old Docker image
   sudo docker images -q aws-project | xargs -r sudo docker rmi -f

   # Build a new Docker image
   sudo docker build -t aws-project .

   # Run a new container on port 8081
   sudo docker run -d -p 8081:80 aws-project


 How to Manually Run the Project
 # Clone the repository
git clone https://github.com/iamzohav/Project-AWS-.git
cd Project-AWS-

# Build the Docker image
sudo docker build -t aws-project .

# Run the container
sudo docker run -d -p 8081:80 aws-project


Access the Application
http://<EC2-PUBLIC-IP>:8081
http://18.60.255.221:8081


 Technologies Used
Jenkins: Automates the CI/CD pipeline.

Docker: Containerizes the application for deployment.

GitHub: Version control and source code management.

AWS EC2: Hosting the Jenkins server and deployed application.

Nginx: Serves the frontend files.

Future Enhancements
Add AWS ECR for container registry.

Implement GitHub Actions for CI/CD.

Use Terraform to automate AWS infrastructure.

Author
Johrabanu Bhandari
