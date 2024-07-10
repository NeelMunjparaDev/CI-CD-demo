pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git 'https://github.com/NeelMunjparaDev/CI-CD-demo.git'
            }
        }
        stage('Build and Test') {
            steps {
                // Set up virtual environment (if needed)
                sh 'python -m venv venv'
                sh '. venv/bin/activate'
                
                // Install dependencies (if any)
                sh 'pip install package1 package2 package3'
                
                // Run unit tests (example)
                sh '. venv/bin/activate && python -m unittest discover'
            }
        }
        stage('Merge to Main') {
            when {
                branch 'main' // Execute only if branch is 'main'
            }
            steps {
                script {
                    // Merge changes into main branch if build is successful
                    def currentBranch = env.BRANCH_NAME
                    if (currentBuild.result == 'SUCCESS') {
                        sh "git checkout main"
                        sh "git merge ${currentBranch}"
                        sh "git push origin main"
                    } else {
                        error "Build or tests failed, cannot merge."
                    }
                }
            }
        }
    }
}
