# Jenkins Pipeline Web Apache Project

A complete CI/CD pipeline for deploying a responsive web application using Jenkins, Docker, and Ansible.

## Project Overview

This project demonstrates a complete DevOps pipeline that:
- Builds a Docker container with an Apache web server
- Deploys a responsive HTML5 website
- Uses Jenkins for CI/CD automation
- Utilizes Ansible for infrastructure automation
- Pushes the Docker image to Docker Hub

## Project Structure

```
jenkins-pipeline-web-apache/
├── Jenkinsfile              # Jenkins pipeline configuration
├── ansible-playbook.yml     # Ansible playbook for deployment
├── Dockerfile              # Docker container configuration
├── README.md              # This file
└── website/               # Web application files
    ├── index.html        # Main HTML page
    ├── config.rb         # Compass/Sass configuration
    ├── css/              # Compiled CSS stylesheets
    ├── sass/             # Sass source files
    ├── js/               # JavaScript files
    ├── img/              # Images and icons
    ├── content/          # Additional content (videos, images)
    ├── fonts/            # Font files
    └── php/              # PHP scripts (contact forms)
```

## Website Features

The web application is a responsive "Coming Soon" page with:
- Modern HTML5/CSS3 design
- Bootstrap framework
- Animated elements and transitions
- Contact form functionality
- Mobile-responsive design
- Google Analytics integration

## Prerequisites

Before running this project, ensure you have:

1. **Jenkins** installed and running
2. **Docker** installed and running
3. **Ansible** installed
4. **Docker Hub account** with credentials configured in Jenkins
5. **Git** for version control

## Jenkins Credentials Setup

1. In Jenkins, create credentials for Docker Hub:
   - Credential ID: `dockerhub-credentials`
   - Type: Username with password
   - Username: Your Docker Hub username
   - Password: Your Docker Hub password or access token

## Running the Pipeline

### Method 1: Jenkins Pipeline (Recommended)

1. **Create a Jenkins Pipeline Job**:
   - Create a new Pipeline job in Jenkins
   - Set the pipeline definition to "Pipeline script from SCM"
   - Choose Git as SCM
   - Enter the repository URL
   - Set the script path to `Jenkinsfile`

2. **Run the Pipeline**:
   - The pipeline will automatically:
     - Log in to Docker Hub using stored credentials
     - Execute the Ansible playbook to build and deploy the container
     - Build the Docker image
     - Push the image to Docker Hub
     - Run the container on port 5000

### Method 2: Manual Execution

If you want to run the steps manually:

1. **Build the Docker image**:
   ```bash
   docker build -t your-dockerhub-username/apache_web_app:v1.0 .
   ```

2. **Run the container**:
   ```bash
   docker run -d --name web-container -p 5000:80 your-dockerhub-username/apache_web_app:v1.0
   ```

3. **Access the website**:
   Open your browser and navigate to `http://localhost:5000`

### Method 3: Using Ansible Playbook

Run the Ansible playbook directly:
```bash
ansible-playbook ansible-playbook.yml
```

## Pipeline Stages

The Jenkins pipeline consists of two main stages:

1. **Docker Login**: Authenticates with Docker Hub using stored credentials
2. **Build & Push Dockerfile**: Executes the Ansible playbook to:
   - Stop any running containers
   - Remove old containers and images
   - Build the new Docker image
   - Push the image to Docker Hub
   - Run the container on port 5000

## Customization

### Changing the Website

To modify the website content:
1. Edit files in the `website/` directory
2. The main page is `website/index.html`
3. Styles can be modified in `website/sass/` or `website/css/`
4. JavaScript functionality is in `website/js/`

### Modifying Docker Configuration

Edit the `Dockerfile` to:
- Change the base image
- Add additional packages
- Modify the web server configuration

### Updating Ansible Playbook

Edit `ansible-playbook.yml` to:
- Change container names or tags
- Modify port mappings
- Add additional deployment steps

## Environment Variables

The pipeline uses the following environment variables:
- `DOCKERHUB_CREDENTIALS_USR`: Docker Hub username (from Jenkins credentials)
- `DOCKERHUB_CREDENTIALS_PSW`: Docker Hub password (from Jenkins credentials)

## Troubleshooting

### Common Issues

1. **Docker login fails**: Check Jenkins credentials configuration
2. **Port 5000 already in use**: Stop other containers using port 5000 or modify the port mapping
3. **Permission denied**: Ensure Docker daemon is running and user has proper permissions

### Logs and Debugging

Check container logs:
```bash
docker logs web-container
```

List running containers:
```bash
docker ps
```

## Security Considerations

- Use Docker Hub access tokens instead of passwords for better security
- Consider using Jenkins secrets management for sensitive data
- Regularly update base Docker images for security patches

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the pipeline
5. Submit a pull request

## License

This project is for educational and demonstration purposes.

## Author

John Bedeir - [johnydev.com](https://johnydev.com)

## Support

For questions or issues, please check the troubleshooting section or create an issue in the repository.
