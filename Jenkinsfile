podTemplate(containers: [
    containerTemplate(
        name: 'ubuntu', 
        image: 'ubuntu:latest', 
        command: 'sleep', 
        args: '30d'
        ),
    containerTemplate(
        name: 'python', 
        image: 'python:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

    node(POD_LABEL) {
        stage('echo test') {
            git url: 'https://github.com/microsoft/AspNetCore-React-WebApp', branch: 'main'
            container('ubuntu') {
                stage('Build service') {
                    sh '''
                    export TZ=Asia/Jerusalem
                    apt-get update -y
                    apt-get install wget -y
                    wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
                    dpkg -i packages-microsoft-prod.deb
                    apt-get update && apt-get install -y dotnet-sdk-6.0
                    rm packages-microsoft-prod.deb
                    ls -la
                    cd service
                    ls 
                    cd ../
                    '''
                }
                stage('Build NPM') {
                    sh '''
                    apt-get update
                    apt-get install nodejs -y 
                    apt-get install npm -y
                    node -v
                    ls -la
                    cd client
                    npm install
                    '''
                }
            }
        }
    }
}
