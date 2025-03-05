pipeline {
    agent any

    environment {
        // Fetching Vercel Token from Jenkins credentials
        VERCEL_TOKEN = credentials('VERCEL_TOKEN')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from your Git repository
                git branch: 'master', url: 'https://github.com/Parvezali4953/Pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                // Build the React app
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Deploy to Vercel using the Vercel CLI
                sh '''
                    echo "Installing Vercel CLI..."
                    npm install -g vercel  # Install Vercel CLI globally
                    echo "Deploying to Vercel..."
                    vercel --prod --token=$VERCEL_TOKEN  # Deploy to production
                '''
            }
        }
    }

}