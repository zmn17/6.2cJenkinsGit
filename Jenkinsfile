pipeline{
    
    agent any
    
    stages {
        stage("Build"){
            steps {
                echo "Build maven project  "
                sh 'mvn clean package'
                sh 'java -cp target/my-maven-app-1.0-SNAPSHOT.jar com.example.App'
            }
        }
        
        stage("Unit and Integration Tests"){
            steps {
                // compile the Java code
                sh 'javac App.java'
                sh 'java -cp .:junit.jar.hamcrest.jar org.junit.runner.JUnitCore AppTest'
            }
        }
        
        stage("Code Analysis"){
            steps {
                // setup SonarQube in Jenkins
                script {
                    // Execute SonarQube analysis
                    withSonarQubeEnv('SonarQubeServer'){
                        sh 'sonar-scanner'
                    }
                }
            }
        }
        
        stage("Security Scan"){
            steps {
                //Run OWASP Dependency Check
                sh 'dependency-check --project mavenProject --scan . --format HTML'
            }
        }
        
        stage("Deploy to Staging"){
            steps {
            	echo "deploy to staging"
            }
        }
        
        stage("Integration Testing on Staging"){
            steps {
            	echo "testing"
            }
        }
        
        stage("Deploy to Production"){
            steps {
            	echo "production"
            }
        }

       post {
        always {
            // Archive generated artifacts and test reports
            archiveArtifacts artifacts: '**/target/*.class', allowEmptyArchive: true
            junit '**/target/test-reports/*.xml'
             }
	}
     }
}