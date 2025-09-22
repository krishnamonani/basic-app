@Library("shared") _
pipeline {
    agent { label "sample-agent" }
    
    stages {
        stage("Code") {
            steps {
                script{
                    clone("https://github.com/krishnamonani/basic-app.git","main")
                }
            }
        }

        stage("Build") {
            steps {
                script{
                    docker_build("sample-app","latest","krishnamonani")
                }
            }
        }


        stage("Push to DockerHub") {
            steps {
                script{
                    docker_push("sample-app","latest","krishnamonani")
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
