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
        stage('SonarQube Analysus '){
            steps {
                sh '''
                    mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                    -Dsonar.projectKey=snake \
                    -Dsonar.projectName='snake' \
                    -Dsonar.host.url=http://13.201.53.173:9000 \
                    -Dsonar.token=sqp_de62c6f7e3b4f56d084636ceb8ffd57d34a68c5b
                '''
            }
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