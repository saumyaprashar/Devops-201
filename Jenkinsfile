node {
   def mvnHome
   def app
   stage('Checkout') { 
      git 'https://github.com/saumyaprashar/DevOps-201-Course.git'
      mvnHome = tool 'MAVEN_HOME'
   }
stage ('Build') {
       sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
   }

stage ('Docker Image Build') {
       app = docker.build("saumyaprashar/devops201:${BUILD_NUMBER}")
}

stage ('Push Docker Image') {
       docker.withRegistry('https://registry.hub.docker.com','docker-credential') {
        		app.push("1-${BUILD_NUMBER}")
        		app.push("latest")
      	}
}

stage('Run Container') {
      sh "sudo docker run -p 8082:8080 -d saumyaprashar/devops201"
}

}
