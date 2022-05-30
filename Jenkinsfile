pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven3" and add it to the path.
        maven "maven3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Gowthamoptit/calcwebapp.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean install package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean install package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the war file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.war'
                }
            }
        }
        stage('tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '0772643b-f884-412e-a9e3-63eb2567206b', path: '', url: 'http://13.58.63.16:8080/')], contextPath: null, war: 'target/*.war'
            }
        }
        stage('tomcat1') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '0772643b-f884-412e-a9e3-63eb2567206b', path: '', url: 'http://35.88.112.238:8080/')], contextPath: null, war: 'target/*.war'
            }
        }
    }
}
