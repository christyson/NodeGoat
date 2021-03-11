pipeline {
  agent {
    docker {
      //image 'node:8.16.0'
      image 'node:8'
    }
  }
  stages {
    stage('Build') {
      steps {
        //sh 'rm -rf node_modules && npm install && npm audit fix --force'
        sh 'rm -rf node_modules && npm install'
      }
    }
    stage('Test') {
      steps {
        // 1.	Enable Veracode Interactive for the steps that run the tests. 
        wrap([$class: 'VeracodeInteractiveBuildWrapper', location: 'host.docker.internal', port: '10010']) {
          // 2.	Download the IAST Agent into the project workspace. 
          sh 'curl -sSL https://s3.us-east-2.amazonaws.com/app.veracode-iast.io/iast-ci.sh |  sh'
          //sh 'chmod +x ./start.sh'
          //sh './start.sh'
          //sh 'chmod +x ./test.sh'
          //sh './test.sh'
          // 3.	Run the tests with the Veracode Interactive Agent attached. 
          //sh ' LD_LIBRARY_PATH=$PWD mocha --require ./agent_nodejs_linux64 test/index.js'
          //sh 'LD_LIBRARY_PATH=$PWD node --require ./agent_linux64.node server.js'
          sh 'LD_LIBRARY_PATH=$PWD npm run test-iast'
          //sh 'LD_LIBRARY_PATH=$PWD npm run test-iast-e23'
          //sh 'LD_LIBRARY_PATH=$PWD npm run test-iast-ci'
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo npm package would run here...'
      }
    }
  }
}
