pipeline {
   agent any
   options {
       ansiColor('xterm')
   }
   stages {
      stage('Clone Git Repository') {
         steps {
             echo "cloning"
            git credentialsId: 'ef6430b2-e140-4c33-a100-1a49c06f4b8a', url: 'https://github.com/nikhilctk/jenkinsdemo.git'
         }
      }
       stage('Test ') {
         steps {
            
            echo "Testing demo " + env.GIT_BRANCH
            
         }
      }
    //   stage('build and deploy') {
    //      steps {
    //          echo "building"
    //        ansiblePlaybook colorized: true, inventory: '/var/jenkins_home/ansible/hosts', playbook: '/var/jenkins_home/ansible/playbook.yml', extras: "--extra-vars 'JOB_NAME=$JOB_NAME'"
    //      }
    //   }
   }
   
   
   post {
    success {
      emailext (
          subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        )
    }

    failure {
      emailext (
          subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        )
    }
  }
}