DevOps Internship Final Assignment: End-to-End CI/CD Pipeline

Project Overview
This project demonstrates an end-to-end DevOps pipeline that builds, containerizes, and deploys a simple web application using GitHub Actions, Docker, and Kubernetes (`k0s`). The application returns a simple message:  
"This is Farhan Shahriar Saying Hello from DevOps”

Tools & Technologies Used
a.	Language:Python (Flask)
b.	CI/CD: GitHub Actions
c.	Containerization: Docker
d.	Container Registry: Docker Hub
e.	Orchestration: Kubernetes (k0s)
f.	VM OS: Ubuntu 18 (VMware)

Project Structure
devops-app/
├── app.py
├── requirements.txt
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── .github/
│ └── workflows/
│ └── ci.yml
└── README.md

Running This Project Locally :
Run without Docker (For Development)
                     pip install -r requirements.txt
                     python3 app.py
                     Visit http://localhost:5000



Run with Docker
Step 1: Build the image
From ~/devops-app:
docker build -t foxtrot10613/devops-app:latest .
Step 2: Run the container
docker run -p 5000:5000 foxtrot10613/devops-app:latest
Then visit http://localhost:5000
CI/CD Workflow Explanation
The CI workflow (.github/workflows/ci.yml) does the following:
1.	Trigger on push to main
2.	Set up Python
3.	Install dependencies
4.	Run basic syntax test (python3 -m py_compile app.py)
5.	Build Docker image
6.	Push to Docker Hub (foxtrot10613/devops-app:latest)
✅ Sample CI Screenshot:
________________________________________
Kubernetes Deployment (k0s)
Deployment & Service YAMLs
•	deployment.yaml: Creates a pod using image from Docker Hub
•	service.yaml: Exposes app via NodePort (e.g., 30007)
Apply the manifests
k0s kubectl apply -f deployment.yaml
k0s kubectl apply -f service.yaml


Access the App
curl http://192.168.19.135:30007

 App is Running via Kubernetes.


What I Learned
•	How to build, tag, and push Docker images to Docker Hub
•	Setting up CI pipelines with GitHub Actions
•	Deploying apps on Kubernetes using k0s
•	Troubleshooting image pull and pod status issues
________________________________________
Challenges Faced
•	ErrImageNeverPull due to local image use — solved by using Docker Hub
•	workflow scope issues with GitHub token — resolved by creating a fine-scoped PAT
•	Service unreachable — fixed by verifying container port and YAML configurations
________________________________________
Future Improvements
•	Add unit tests to improve CI
•	Integrate CD via ArgoCD or GitHub Actions to auto-deploy on merge
•	Use ingress controller for better access in K8s
________________________________________
Links
•	 GitHub Repository: https://github.com/f-oxtrot/devops-app
•	 Docker Hub Image: https://hub.docker.com/r/foxtrot10613/devops-app


