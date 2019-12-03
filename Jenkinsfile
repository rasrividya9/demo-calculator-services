node {
    def app

    stage('Checkout') {
        checkout scm
    }
	
    stage('Maven Package') {
        withMaven(maven:'maven-3.6.3'){
          sh 'mvn clean package'
	}
    }

    stage('Build image') {
        app = docker.build("demo-calculator-service")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhubcredentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

