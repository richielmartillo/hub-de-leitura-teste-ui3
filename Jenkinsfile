pipeline {
    agent any

    tools {
        nodejs "nodejs"
    }

    stages {

        stage("Clonar o hub de leitura integrado") {
            steps {
                bat '''
                    if exist hub-de-leitura-integrado2 rmdir /s /q hub-de-leitura-integrado2
                    git clone --depth 1 https://github.com/EBAC-QE/hub-de-leitura-integrado2.git
                '''
            }
        }

        stage("Instalar dependencias e subir aplicacao") {
            steps {
                dir('hub-de-leitura-integrado2') {
                    bat '''
                        call npm ci
                        start /B npm start
                    '''
                }
            }
        }

        stage("Clonar o projeto de teste") {
            steps {
                bat '''
                    if exist hub-de-leitura-teste-ui2 rmdir /s /q hub-de-leitura-teste-ui2
                    git clone --depth 1 https://github.com/EBAC-QE/hub-de-leitura-teste-ui2.git
                '''
            }
        }

        stage("Instalar dependencias do projeto de teste") {
            steps {
                dir('hub-de-leitura-teste-ui2') {
                    bat 'call npm ci'
                }
            }
        }

        stage("Esperar a aplicacao subir") {
            steps {
                dir('hub-de-leitura-teste-ui2') {
                    bat 'npx wait-on http://localhost:3000'
                }
            }
        }

        stage("Executar testes no Cypress Cloud") {
            steps {
                dir('hub-de-leitura-teste-ui2') {
                    withCredentials([string(credentialsId: 'cypress-record-key', variable: 'CYPRESS_RECORD_KEY')]) {
                        bat '''
                            npx cypress run ^
                            --record ^
                            --key %CYPRESS_RECORD_KEY% ^
                            --browser chrome ^
                            --ci-build-id jenkins-%BUILD_NUMBER% ^
                            --group "UI-Windows"
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            dir('hub-de-leitura-teste-ui2') {
                archiveArtifacts artifacts: 'cypress/screenshots/**/*.*,cypress/videos/**/*.*', allowEmptyArchive: true
                allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
            }

            bat '''
                taskkill /F /IM node.exe >nul 2>&1
                exit /b 0
            '''
        }
    }
}