# EventsProject Monitoring and Dockerization 🐳📊

This repository provides a Dockerized setup for the EventsProject, a Spring Boot backend application, along with a comprehensive monitoring infrastructure.

## Application Structure 📁

The application consists of a Spring Boot backend located within the `app` folder.

### Project Directory

```
EventsProject/
│
├── app/
│   ├── backend/
│   │   ├── src/
│   │   ├── pom.xml
│   │   └── Dockerfile
│
├── infrastructure/
│   └── docker-compose.yml
│
└── README.md
```

## Infrastructure Setup 🛠️

The `infrastructure` folder contains a Docker Compose file that sets up the following monitoring and CI/CD services:

- Jenkins
- Grafana
- Prometheus
- Nexus
- Node Exporter
- MySQL Exporter
- SonarQube

### Jenkins 🛠️

- **Image:** `jenkins/jenkins:lts`
- **Container Name:** `jenkins`
- **Ports:** `8080:8080`, `50000:50000`
- **Volumes:** `./jenkins_home:/var/jenkins_home`
- **Networks:** `backend-network`
- **Access:** [http://localhost:8080](http://localhost:8080)
- **Notes:** Jenkins home directory is persisted at `./jenkins_home`

### Grafana 📊

- **Image:** `grafana/grafana`
- **Container Name:** `grafana`
- **Ports:** `3000:3000`, `9090:9090`
- **Volumes:** `./grafana:/var/lib/grafana`
- **Networks:** `backend-network`
- **Access:** [http://localhost:3000](http://localhost:3000)
- **Notes:** Grafana configuration and data are persisted at `./grafana`

### Prometheus 📈

- **Image:** `prom/prometheus`
- **Container Name:** `prometheus`
- **Ports:** `8090:8090`
- **Volumes:** `./prometheus:/etc/prometheus`, `./prometheus/data:/prometheus`
- **Networks:** `backend-network`
- **Access:** [http://localhost:8090](http://localhost:8090)
- **Notes:** Prometheus configuration and data are persisted at `./prometheus`

### Nexus 🛠️

- **Image:** `sonatype/nexus3`
- **Container Name:** `nexus`
- **Ports:** `8081:8081`
- **Volumes:** `./nexus-data:/nexus-data`
- **Networks:** `backend-network`
- **Access:** [http://localhost:8081](http://localhost:8081)
- **Notes:** Nexus configuration and data are persisted at `./nexus-data`

### Node Exporter 📊

- **Image:** `prom/node-exporter`
- **Container Name:** `node-exporter`
- **Ports:** `9100:9100`
- **Networks:** `backend-network`

### MySQL Exporter 📈

- **Image:** `prom/mysqld-exporter`
- **Container Name:** `mysql-exporter`
- **Ports:** `9104:9104`
- **Environment Variables:** `DATA_SOURCE_NAME: "user:password@(host:port)/"`
- **Networks:** `backend-network`

### SonarQube 🛠️

- **Image:** `sonarqube`
- **Container Name:** `sonarqube`
- **Ports:** `9000:9000`
- **Networks:** `backend-network`
- **Access:** [http://localhost:9000](http://localhost:9000)

## Usage 🚀

### Application Setup

1. Navigate to the `app/backend` directory.
2. Ensure your Spring Boot backend application (`EventsProject`) is correctly configured.

### Infrastructure Setup

1. Navigate to the `infrastructure` directory.
2. Run `docker-compose up -d` to start the infrastructure services.

### Running the Application

1. Navigate to the `app` directory.
2. Run `docker-compose up -d` to start the backend services.

### Access Your Services

- **Backend:** [http://localhost:8089](http://localhost:8089)
- **Grafana:** [http://localhost:3000](http://localhost:3000)
- **Prometheus:** [http://localhost:9090](http://localhost:8090)
- **Jenkins:** [http://localhost:8080](http://localhost:8080)
- **Nexus:** [http://localhost:8081](http://localhost:8081)
- **SonarQube:** [http://localhost:9000](http://localhost:9000)

## Notes 📓

- Ensure Docker and Docker Compose are installed on your machine.
- Update any service configurations as needed in the `docker-compose.yml` file.
- Use the volumes to persist data for Jenkins, Grafana, Prometheus, and Nexus.

## Monitoring Setup 📊

Grafana and Prometheus are set up to provide real-time monitoring and alerting for the EventsProject. 

- **Grafana:** Visualize metrics and logs in a customizable dashboard.
- **Prometheus:** Collect and store metrics from Node Exporter and MySQL Exporter.
- **Node Exporter:** Monitor system metrics.
- **MySQL Exporter:** Monitor MySQL database metrics.

### Setting Up Dashboards

1. Access Grafana at [http://localhost:3000](http://localhost:3000).
2. Log in with the default credentials (`admin/admin`).
3. Add Prometheus as a data source (URL: `http://prometheus:8090`).
4. Import pre-configured dashboards or create custom dashboards to monitor the health and performance of your application and infrastructure.

Enjoy your Dockerized EventsProject setup with comprehensive monitoring! 🐳📊