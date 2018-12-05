#!groovy
node('ra-skx-32') {
  withEnv(['DB_ENGINE=sqlite']) {
    try {
      stage('setup_workspace') {
      
        if (!env.CHANGE_ID) {
          // echo "ENGINE ${ENGINE}"
          echo "env.CHANGE_ID: ${env.CHANGE_ID}" 
        }
        
        if (!env.BUILD_NUMBER) {
          echo "env.BUILD_NUMBER: ${env.BUILD_NUMBER}" 
        }
        
        def container_name = null
        if (env.CHANGE_ID && env.BUILD_NUMBER) {
          container_name = "nnpi-transformer__${env.CHANGE_ID}__${env.BUILD_NUMBER}"
        } else if (BRANCH_NAME == "master") {
          container_name = "master_" + new Date().getTime().toString()
        }
        echo "container_name ${container_name}"
        
        echo "env.tag: ${env.tag}" 
        echo "tag: ${tag}" 
        
        sh 'pwd && ls -la'
        //deleteDir()
        echo 'checking out scm'
        checkout scm
        echo 'checkout scm'
        // ERROR: ‘checkout scm’ is only available when using “Multibranch Pipeline” or “Pipeline script from SCM”
        sh 'pwd && ls -la'
        //sh 'echo "build output" >> ./build_output.txt'
        //sh 'pwd && ls -la'
      }
    } finally {
      sh 'ls -la ${WORKSPACE}'
      echo env.dump()
      echo env.JOB_NAME
    }
  }
}
