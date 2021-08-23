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
	post{
		failure{
                mail to: 'sonitgupta7@gmail.com',
                from: 'sonitgupta7@gmail.com',
                Subject: "Project Build: ${env.JOB_NAME} - Failed",
                body: "Job Failed -  \ "${env.JOB_NAME} \" build: ${env.BUILD_NUMBER}"
            }
		success{
                    emailext attachPattern: "*target/*.war",
                    body: '''${SCRIPT, template="groovy-template"}''',
                    subject: "Project Build: ${env.JOB_NAME} - SUCCESS",
                    mimeType: 'text/html',
                    to: 'sonitgupta7@gmail.com'
            }
	}
}
