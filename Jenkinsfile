pipeline {
    agent any
    
    stages {
        
        stage('Clean Source Repo') {
            steps {
                bat '''
                if exist Jenkins_pipeline (
                    rmdir /s /q Jenkins_pipeline
                )
                '''
            }
        }

        stage('Clone Source Repo') {
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

        stage('Commit & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'githubtoken', usernameVariable: 'USER', passwordVariable: 'TOKEN')]) {
                    bat '''
                    git config user.email "dhruvmarwal304@gmail.com"
                    git config user.name "DhruvMarwal"
                    git add .
                    git commit -m "Auto copied files from Kapil repo" || exit 0
                    git push https://%USER%:%TOKEN%@github.com/DhruvMarwal/Jenkins_.git HEAD:main
                    '''
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
