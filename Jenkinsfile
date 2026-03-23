pipeline {
    agent any
 
    stages {
        stage('Clean Kapil Repo') {
            steps {
                bat '''
                if exist Jenkins_pipeline (
                    rmdir /s /q Jenkins_pipeline
                )
                '''
            }
        }
 
        stage('Clone Kapil Repo') {
            steps {
                bat 'git clone https://github.com/kapilrahtor/Jenkins_pipeline.git'
            }
        }
 
        stage('Copy Files to My Repo') {
            steps {
                bat '''
                robocopy Jenkins_pipeline . /E /XD .git
                if %ERRORLEVEL% LEQ 7 exit /B 0
                '''
            }

        }
 
        stage('Commit & Push to My Repo') {

            steps {

                withCredentials([usernamePassword(credentialsId: 'github-token', usernameVariable: 'USER', passwordVariable: 'TOKEN')]) {

                    bat 'git config user.email "jenkins@lab.com"'

                    bat 'git config user.name "Jenkins"'

                    bat 'git add .'

                    bat 'git commit -m "Auto copied files from Kapil repo" || exit 0'

                    bat 'git push https://%USER%:%TOKEN%@github.com/DhruMarwal/Jenkins_.git HEAD:main'
                }

            }

        }
 
        stage('Build') {

            steps {

                bat 'Build.bat'

            }

        }
 
        stage('Test') {

            steps {

                bat 'Test.bat'

            }

        }
 
        stage('Deploy') {

            steps {

                bat 'Deploy.bat'

            }

        }
 
    }

}
 
