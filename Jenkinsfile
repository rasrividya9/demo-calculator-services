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
        app = docker.build("demo-calculator-services")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com/rasrividya9/demo-calculator-services', 'dockerhubcredentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

