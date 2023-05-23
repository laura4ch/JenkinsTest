pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'installing pip deps..'
                
                git credentialsId: 'laura', branch: 'main', url: 'https://github.com/mtararujs/python-greetings'
          
                bat "dir" 
          
                bat "pip install -r requirements.txt"
                
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'deploying to dev..'
                deploy("DEV", 7001)
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'testsing on dev..'
                test("dev")
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'deploying to staging..'
                deploy("STAGING", 7002)
            }
        }
         stage('tests-on-staging') {
            steps {
                echo 'testsing on staging..'
                test("staging")
            }
        }
         stage('deploy-to-preprod') {
            steps {
                echo 'deploying to preprod..'
                deploy("PREPROD", 7003)
            }
        }
         stage('tests-on-preprod') {
            steps {
                echo 'testsing on preprod..'
                test("preprod")
            }
        }
         stage('deploy-to-prod') {
            steps {
                echo 'deploying to prod..'
                deploy("PROD", 7004)
            }
        }
         stage('test-on-prod') {
            steps {
                echo 'testing on prod..'
                test("prod")
            }
        }
    }
}



def deploy(String enviroment, int port){
   git credentialsId: 'laura', branch: 'main', url: 'https://github.com/mtararujs/python-greetings' 
   bat "pm2 delete greetings-app-${enviroment} & EXIT /B 0)"
   bat "pm2 start app.py --name greetings-app-${enviroment} -- --port ${port}"
   
}


def test(String enviroment){
   git credentialsId: 'laura', branch: 'main', url: 'https://github.com/mtararujs/course-js-api-framework' 
   bat "npm install"
   bat "npm run greetings greetings_${enviroment}"
    
}

