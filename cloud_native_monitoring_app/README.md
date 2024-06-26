# Cloud Native Resource Monitoring Python App on K8
![App Screenshot](https://miro.medium.com/v2/resize:fit:2000/1*_cu-mK1XnWbYIhKlW-Z9Xw.jpeg)

## Part 1: Deploying the Flask application

1. Install AWS CLI using the below link: 
```bash
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
```

2. Connect with AWS:
```bash
aws configure
```

3. Clone the code from the repository:
```bash
git clone <repository_url>
```

4. Install dependencies:
```bash
pip3 install -r requirements.txt
```

5. Run the application:
```bash
python3 app.py
```

## Part 2: Dockerizing the Flask application

1. To build the Docker image from the Dockerfile, execute the following command:
```bash
docker build -t <image_name> .
```

2. To run the Docker container, execute the following command:
```bash
docker run -p 5001:5001 <image_name>
```

3. Navigate to http://localhost:5001/ on your browser to access the application.

## Part 3: Pushing the Docker image to ECR

1. The ECR repository is created using Python boto3 AWS SDK as seen in the ecr.py file.

2. Run the code using the below command:
```bash
python3 ecr.py
```

3. In AWS, click on 'View Push Commands' in the ECR repo console. Paste the commands shown one by one in the local terminal. This will push the Docker image from the local machine to the ECR.

## Part 4: Creating an EKS cluster and deploying the app using Python

1. Create an EKS cluster and a node group in the AWS account

2. Update your kubeconfig file to include your EKS cluster using the AWS CLI:
```bash
aws eks update-kubeconfig --region <your-region> --name <your-cluster-name>
```

3. The Deployment and Service are specified in eks.py file. Edit the name of the image in this file with your image Uri.

4. Run this file using the below command so that deployment and service will be created.
```bash
python3 eks.py
```

4. Check by running following commands:
```bash
kubectl get deployment -n default 
kubectl get service -n default 
kubectl get pods -n default 
```

5. Once your pod is up and running, run the port-forward to expose the service
```bash
kubectl port-forward service/<service_name> 5001:5001
```
