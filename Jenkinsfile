node {
  stage "Git pull"
    git url: 'https://github.com/wongchunhung/pythonapp.git'
    sh 'git checkout test'
    sh 'git clean -f'
    sh 'git reset'
    sh 'git stash'
    sh 'git pull'

  stage "Docker Build"
    sh 'docker build -t chunha/pythonapp:0.1.${BUILD_NUMBER} .'

  stage "Git clean"
    sh 'git clean -f'

  stage "Unit test"
    echo "unit test..."

  stage "Integration test"
    echo "Integration test..."

  stage "Image Push"
    withCredentials([usernamePassword(credentialsId: 'harbor', passwordVariable: 'harborPassword', usernameVariable: 'harborUser')]) {
      sh "docker login -u ${env.harborUser} -p ${env.harborPassword} ingress.k8s-1.local"
      sh 'docker tag chunha/pythonapp:0.1.${BUILD_NUMBER} ingress.k8s-1.local/chunha/pythonapp:0.1.${BUILD_NUMBER}'
      sh 'docker push ingress.k8s-1.local/chunha/pythonapp:0.1.${BUILD_NUMBER}'
    }

  stage "Deployment"
    build job: 'pythonapp_k8s_deploy', parameters: [[$class: 'StringParameterValue', name: 'BUILD', value: BUILD_NUMBER]]
}
