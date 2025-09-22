@Library("shared") _
pipeline {
    agent { label "sample-agent" }
    
    stages {
        stage("Code") {
            steps {
                echo "This is cloning the code."
                git url: "https://github.com/krishnamonani/basic-app.git", branch: "main"
                echo "Code Cloned Successfully."
            }
        }

        stage("Build") {
            steps {
                echo "This is building the code."
                sh "whoami"
                sh "docker build -t sample-app ."
            }
        }

        // stage("Run") {
        //     steps {
        //         sh '''
        //              # Stop and remove old container (running or stopped) if it exists
        //             docker ps -aq --filter "name=sample-container" | grep -q . && docker stop sample-container && docker rm sample-container || true
            
        //             # Run fresh container
        //             docker run -d -p 5000:5000 --name sample-container sample-app
        //             '''
        //     }
        // }
        stage("Push to DockerHub") {
            steps {
                echo "Pushing the image to DockerHub"
                withCredentials([usernamePassword('credentialsId': "dockerhub-cred", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh '''
                        echo "$dockerHubPass" | docker login -u "$dockerHubUser" --password-stdin
                        docker image tag sample-app $dockerHubUser/sample-app:latest
                        docker push $dockerHubUser/sample-app:latest
                    '''
                }
            }
        }
        stage("Deploy App") {
            steps {
                deploy() // Uses default docker-compose.yml
            }
        }
        stage('Verify App') {
            steps {
                sh 'curl -f http://localhost:5000 || exit 1'
            }
        }
    }
}
