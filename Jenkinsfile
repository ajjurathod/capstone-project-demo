node{
    stage('code checkout'){
        git 'https://github.com/ajjurathod/capstone-project-demo.git'
    }
    stage('build'){
        sh 'mvn clean package'
    }
    stage('conatinerization'){
        sh 'docker build -t ajjurathod1998/insure-me:1.0 .'
        
    }
    
    stage('pushing to dockerhub'){
        withCredentials([string(credentialsId: 'dockerPwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u ajjurathod1998 -p ${dockerHubPwd}"
        sh "docker push ajjurathod1998/insure-me:1.0"
      }
    }
    
    stage('deploy'){
      ansiblePlaybook become: true, credentialsId: 'ansible-ssh-project-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
    }
}
