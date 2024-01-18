pipeline {
  agent {label 'slave3'}
  stages {
  stage ('checkout') {
    steps {
      sh 'rm -rf Parcel-service'
      sh 'git clone https://github.com/yatheesh2328/Parcel-service.git'
    }
  }
  stage ('build') {
    steps {
      sh 'mvn --version'
      sh 'mvn clean install'
    }
  }
    stage ('deploy') {
      steps {
        sh 'scp /home/slave3/workspace/demoMBP2_feature-2/target/simple-parcel-service-app-1.0-SNAPSHOT.jar root@172.31.17.229:/opt/apache-tomcat-8.5.98/webapps/'
}
}
  }
}
