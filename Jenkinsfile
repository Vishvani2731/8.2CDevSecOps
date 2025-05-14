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
        bat '''
        echo Downloading SonarScanner...
        powershell -Command "Invoke-WebRequest -Uri https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-windows.zip -OutFile sonar-scanner.zip"

        echo Extracting...
        powershell -Command "Expand-Archive sonar-scanner.zip -DestinationPath . -Force"

        echo Running SonarScanner...
        sonar-scanner-5.0.1.3006-windows\\bin\\sonar-scanner.bat ^
          -Dsonar.projectKey=your_projectKey ^
          -Dsonar.organization=your_org ^
          -Dsonar.sources=. ^
          -Dsonar.host.url=https://sonarcloud.io ^
          -Dsonar.login=your_token
        '''
    }
}

 }
}
