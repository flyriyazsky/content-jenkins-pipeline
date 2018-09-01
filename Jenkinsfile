@Library('pipeline-lib')

node {
agent any
 stages {
 
 stage('Git Clone App') {
        def projectName = new utils().getProjectName()
            sh "git clone git@https://github.com/flyriyazsky/${projectName}.git -b ${env.BRANCH_NAME} ."
        } 
  
  
 stage('build') {
 steps {
 sh 'javac -d . src/*.java'
 sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
 sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
 }
 }
 stage('run') {
 steps {
 sh 'java -jar rectangle.jar 7 9'
 }
 }
 }
 post {
 success {
 archiveArtifacts artifacts: 'rectangle.jar', fingerprint:
true
 }
 }
}
