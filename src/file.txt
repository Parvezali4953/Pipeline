pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('VERCEL_TOKEN')  // Fetching Vercel Token from Jenkins credentials
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Parvezali4953/Pipeline.git'  // Replace with your GitHub repo
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'  // Builds the React project
            }
        }

        stage('Deploy to Vercel') {
            steps {
                sh '''
                    npm install -g vercel  # Install Vercel CLI globally
                    vercel --prod --token=$VERCEL_TOKEN  # Deploying to Vercel
                '''
            }
        }
    }
}
