pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        sh 'aws s3 cp build/libs/application.war s3://jenkins-ci-cd-application/application.war --region ap-northeast-2'
      }
    }

    stage('deploy') {
      steps {
        sh 'aws elasticbeanstalk create-application-version --region ap-northeast-1 --application-name ElasticBeansTalk_Test_01 --version-label ${BUILD_TAG} --source-bundle S3Bucket="jenkins-ci-cd-application",S3Key="application.war"'
        sh 'aws elasticbeanstalk update-environment --region ap-northeast-1 --environment-name Elasticbeanstalktest01-env --version-label ${BUILD_TAG}'
      }
    }

  }
}
