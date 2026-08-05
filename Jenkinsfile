pipeline{
    agent any 

    tools {
        jdk 'java-17'
        maven 'maven'
    }
    stages{
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/Thejas821/snake.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                sh '''
                    mvn compile
                '''
            }
        }

        stage('Packaging') {
            steps {
                sh '''
                    mvn clean package
                '''
            }
        }
        post {
        always {
            // Generates and displays the JaCoCo coverage report in Jenkins
            jacoco(
                execPattern: '**/target/*.exec',
                classPattern: '**/target/classes',
                sourcePattern: '**/src/main/java',
                exclusionPattern: '**/*Test.class'
            )
        }
    }
    }       
}
