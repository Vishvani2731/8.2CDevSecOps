pipeline {
 agent any
 stages {
 stage('Checkout') {
 steps {
 git branch: 'main', url: ' https://github.com/Vishvani2731/8.2CDevSecOps.git'
 }
 }
 stage('Install Dependencies') {
 steps {
 bat 'npm install'
 }
 }
 stage('Run Tests') {
 steps {
 bat 'npm test || exit /b 0' // Allows pipeline to continue despite test failures
 }
 }
 stage('Generate Coverage Report') {
 steps {
 // Ensure coverage report exists
 bat 'npm run coverage || exit /b 0'
 }
 }
 stage('NPM Audit (Security Scan)') {
 steps {
 bat 'npm audit || exit /b 0' // This will show known CVEs in the output
 }
 }
  stage('SonarCloud Analysis') {
            steps {
                sh '''
                echo "Downloading SonarScanner..."
                curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
                unzip -q sonar-scanner.zip
                export PATH=$PWD/sonar-scanner-5.0.1.3006-linux/bin:$PATH

                echo "Running SonarScanner..."
                sonar-scanner \
                  -Dsonar.projectKey=your_project_key \
                  -Dsonar.organization=your_organization \
                  -Dsonar.sources=. \
                  -Dsonar.host.url=https://sonarcloud.io \
                  -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }
 }
}
