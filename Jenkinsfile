pipeline{
    agent any
    stages{
        stage ('checkout the code from SCM'){
            steps{
                echo 'checkout the code'
            }
        }
        stage ('Build the project'){
            steps{
                echo 'building the project'
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Sonarqube'){
            steps{
                echo 'Sonar Codequality'
                sh '''
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=Mobilestore \
                -Dsonar.host.url=http://51.120.240.173:9000 \
                -Dsonar.login=sqp_e00ab32ba1546496a14f42cd4daad925a03975eb
           '''
            }
        }
        stage('Deploy to dev'){
            steps{
                echo "Deploying to dev environment"
                sh 'docker rm -f mobile || true'
                sh 'docker run -d --name=mobile -p 8099:8099 mobilestore'
            }
        }


    }
}
