podTemplate(containers: [
    containerTemplate(name: 'angular', image: 'pivotalpa/angular-cli:latest', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'maven', image: 'golang:1.8.0', ttyEnabled: true, command: 'cat')
  ]) {

    node(POD_LABEL) {
        stage('Get a Npm project') {
            git 'https://github.com/victor-tns/lazy-load-front.git'
            container('angular') {
                stage('Build a Npm project') {
                    sh 'npm install'
                }
            }
        }

        stage('Get a Golang project') {
            git url: 'https://github.com/victor-tns/lazy-load-backend.git'
            container('maven') {
                stage('Build a Maven project') {
                    sh """
                        chmod +x gradlew
                        gradlew build -x test
                    """
                }
            }
        }

    }
}
