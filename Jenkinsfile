pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        bat(script: ' %workingDir%/create_build.bat --branchName=%branchName% --targetTag=%targetTag% --originTag="%originTag%" --sourceDir=%workingDir%', label: 'Checkout')
      }
    }

    stage('Code Quality Gate') {
      steps {
        echo 'test scan'
      }
    }

    stage('Build & Package') {
      steps {
        bat(script: '%workingDir%/create_build.bat --branchName=%branchName% --targetTag=%targetTag% --originTag="%originTag%" --sourceDir=%workingDir% --createBuild=true', label: 'Create Build')
      }
    }

  }
  environment {
    branchName = 'master'
    targetTag = '13703'
    originTag = ''
    workingDir = 'C:\\Apps\\jenkins\\workspace\\PWC_Pipeline_Build_Dep'
  }
  parameters {
    string(name: 'branchName', defaultValue: 'master', description: 'Branch Name')
  }
}