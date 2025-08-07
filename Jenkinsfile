pipeline {
  agent any

  environment {
    NODE_ENV = 'development'
  }

  stages {
    stage('Clean Workspace') {
      steps {
        deleteDir() // Clean everything
      }
    }

    stage('Clone Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/YohannesTsegaye/smart.git'
      }
    }

    stage('Install Frontend Dependencies') {
      steps {
        dir('frontend') {
          sh 'npm ci'
        }
      }
    }

    stage('Verify react-hot-toast Installed') {
      steps {
        dir('frontend') {
          sh 'ls node_modules/react-hot-toast || echo "❌ react-hot-toast not found"'
        }
      }
    }

    stage('Build Frontend') {
      steps {
        dir('frontend') {
          sh 'npm run build'
        }
      }
    }

    stage('Install Backend Dependencies') {
      steps {
        dir('backend') {
          sh 'npm ci'
        }
      }
    }

    stage('Build Backend') {
      steps {
        dir('backend') {
          sh 'npm run build'
        }
      }
    }

    stage('Test Backend') {
      steps {
        dir('backend') {
          sh 'npm run test'
        }
      }
    }

    stage('Start Backend') {
      steps {
        dir('backend') {
          sh 'npm run start'
        }
      }
    }

    stage('Start Frontend') {
      steps {
        dir('frontend') {
          sh 'npm start'
        }
      }
    }
  }

  post {
    failure {
      echo "❌ Build failed! Check errors above."
    }
    success {
      echo "✅ Build completed successfully!"
    }
  }
}
