podTemplate(containers: [
    containerTemplate(name: 'angular', image: 'pivotalpa/angular-cli:latest', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'gradle', image: 'gradle:jdk8-alpine', ttyEnabled: true, command: 'cat')
  ]) {

    node(POD_LABEL) {
        stage('Get a Gradle project') {
            git url: 'https://github.com/victor-tns/lazy-load-backend.git'
            container('gradle') {
                stage('Build a Gradle project') {
                    sh """
                        gradle build -x test
                    """
                }
            }
        }
        stage('Get a Npm project') {
            git 'https://github.com/victor-tns/lazy-load-front.git'
            container('angular') {
                stage('Build a Npm project') {
                    sh 'npm install'
                }
            }
        }    

    }
}
