pipeline {
    agent any

    environment {
        AEM_AUTHOR = 'http://localhost:4502'
        AEM_USER = 'admin'
        AEM_PASSWORD = 'admin'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build AEM Project') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy to AEM Author') {
            steps {
                script {
                    def pkg = 'all/target/globaluniversity-aem.all-1.0.0-SNAPSHOT.zip'

                    // Upload
                    sh """
                    curl -u $AEM_USER:$AEM_PASSWORD -F package=@$pkg \\
                    $AEM_AUTHOR/crx/packmgr/service.jsp?cmd=upload
                    """

                    // Install
                    sh """
                    curl -u $AEM_USER:$AEM_PASSWORD \\
                    $AEM_AUTHOR/crx/packmgr/service.jsp?cmd=install&name=globaluniversity-aem.all-1.0.0-SNAPSHOT.zip
                    """
                }
            }
        }
    }
}
