pipeline {
    agent any

    tools {
        maven 'Maven_3.9.11' // Adjust this name to match your Maven installation in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/SanjanaBhandarkar24/globaluniversity-aem'
            }
        }

        stage('Build AEM Project') {
            steps {
                dir('globaluniversity') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Deploy to AEM Author') {
            steps {
                dir('globaluniversity') {
                    sh '''
                        echo "Checking package file:"
                        ls -lh all/target

                        curl -u admin:admin \
                        -F package=@all/target/globaluniversity.all-1.0.0-SNAPSHOT.zip \
                        http://localhost:4502/crx/packmgr/service.jsp?cmd=upload
                    '''
                }
            }
        }
    }
}
