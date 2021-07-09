pipeline{
        agent any
        environment {
                DB_PASSWORD = credential("DB_PASSWORD")
        }
        stages{
                stage('Clone repo') {
                        steps {
                                script {
                                        sh "rm -rf chaperootodo_client"
                                        sh "git clone https://gitlab.com/qacdevops/chaperootodo_client"
                                }
                        }
                }
               stage('Install dependencies'){
                        steps {   
                                script {
                                        sh "curl https://get.docker.com | sudo bash"
                                        sh 'sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                                        sh "sudo chmod +x /usr/local/bin/docker-compose"
                                }
                        }
               }
              stage('Deploy app'){
                        steps { 
                                script { 
                                        sh "cd chaperootodo_client && sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d"
                                }
                        }
              }
        }
}
