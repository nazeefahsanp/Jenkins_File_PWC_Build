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
        bat(script: '%workingDir%/%targetTag%/buildscripts/build_engine/build.bat %targetTag% %workingDir% %originTag% ', label: 'Delta Extraction')
        bat(script: '%workingDir%/%targetTag%/buildscripts/build_engine/build_transformation.bat %branchName% %targetTag% %workingDir% %originTag%', label: 'Transformation')
        bat(script: '%workingDir%/%targetTag%/buildscripts/build_engine/build_compilation.bat %branchName% %targetTag% %workingDir% %originTag%', label: 'Compilation')
      }
    }

  }
  environment {
    branchName = 'master'
    targetTag = '13672'
    originTag = '13671'
    workingDir = 'C:\\Apps\\jenkins\\workspace\\PWC_Pipeline_Build_Dep'
  }
  parameters {
    string(name: 'branchName', defaultValue: 'master', description: 'Branch Name')
  }
}