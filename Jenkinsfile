pipeline{
    agent any
    triggers{
        githubPush()
    }
    environment{
        PATH ="C:\\Program Files\\Docker\\Docker\\resources\\bin;${env.PATH}"
        IMAGE_NAME = "sinav-test"
        CONTAINER_NAME ="nginx-test"
    }
    stages{
        stage('repoyu klonla'){
            steps{
            git url:'https://github.com/13ilge/sinav.git', branch:'main'
            }
        }
         stage('docker image olustur'){
            steps{
                echo "docker ı-image olusturuldu"
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }
        stage('eski containeri durdur'){
            steps{
                echo "eski cont durduruldu"
                bat "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        stage('yeni containeri olustur'){
            steps{
                echo "yeni cont olusturuldu"
                bat "docker run -d --name ${CONTAINER_NAME} -p 4444:80 ${IMAGE_NAME}"
            }
        }
    }
    post{
        success{
            echo "yayın basarili"
        }
        failure{
            echo "yayin basarisiz"
        }
    }
    
}
