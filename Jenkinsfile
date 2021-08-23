pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Checkout SCM'){
            steps{
                git url: 'https://github.com/falcon-18-tech/Jenkins_Spring.git'
            }
        }
        stage('Build'){
            steps{
                echo "Running Job: ${env.JOB_NAME}\n build: ${env.BUILD_ID}"
                sh 'mvn -f ./pom.xml clean install package'
            }
            post{
                success{
                    archiveArtifacts(artifacts: 'Jenkins_Spring/target/*.war', allowEmptyArchive: true)
                }
            }
	}
    }
}
