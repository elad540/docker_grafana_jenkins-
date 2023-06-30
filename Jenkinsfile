pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        // Clone your repository or obtain the necessary code
        // Perform any build steps if required
      }
    }

    stage('Deploy') {
      steps {
        script {
          // Start Grafana Docker container
          if (isUnix()) {
            sh 'docker run -d --name grafana-container -p 3000:3000 grafana/grafana:latest'
          } else {
            bat 'docker run -d --name grafana-container -p 3000:3000 grafana/grafana:latest'
          }
        }
      }
    }

    stage('Import Dashboards') {
      steps {
        script {
          // Wait for Grafana to start
          if (isUnix()) {
            sh 'sleep 20'
          } else {
            bat 'ping 127.0.0.1 -n 21 > nul'
          }

          // Import built-in dashboards
          if (isUnix()) {
            sh 'docker exec -i grafana-container grafana-cli plugins install grafana-clock-panel'
            sh 'docker exec -i grafana-container grafana-cli plugins install grafana-simple-json-datasource'
            sh 'docker exec -i grafana-container grafana-cli plugins install grafana-worldmap-panel'
            sh 'docker exec -i grafana-container grafana-cli plugins install grafana-piechart-panel'
            sh 'docker exec -i grafana-container grafana-cli plugins install grafana-polystat-panel'
          } else {
            bat 'docker exec -i grafana-container grafana-cli plugins install grafana-clock-panel'
            bat 'docker exec -i grafana-container grafana-cli plugins install grafana-simple-json-datasource'
            bat 'docker exec -i grafana-container grafana-cli plugins install grafana-worldmap-panel'
            bat 'docker exec -i grafana-container grafana-cli plugins install grafana-piechart-panel'
            bat 'docker exec -i grafana-container grafana-cli plugins install grafana-polystat-panel'
          }
        }
      }
    }

    stage('Test') {
      steps {
        // Run any tests against the Grafana instance
      }
    }

    stage('Cleanup') {
      steps {
        script {
          // Stop and remove the Grafana Docker container
          if (isUnix()) {
            sh 'docker stop grafana-container'
            sh 'docker rm grafana-container'
          } else {
            bat 'docker stop grafana-container'
            bat 'docker rm grafana-container'
          }
        }
      }
    }
  }
}


