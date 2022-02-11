pipeline {
    agent any
    
    tools
    {
       maven "Maven"
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/mahantheshmr/CI-usingAnsible.git'
             
          }
        }
         stage('Tools Init') {
            steps {
                script {
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               def tfHome = tool name: 'Ansible'
                env.PATH = "${tfHome}:${env.PATH}"
                 sh 'ansible --version'
                    
            }
            }
        }
     
        
         stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        
        
         
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
             
               
               //sh "ansible-playbook main.yml -i inventories/dev/hosts --user jenkiins --key-file ~/.ssh/id_rsa"
               // sh "ansible-playbook main.yml -i inventories/dev/hosts -u ec2-user"
               ansiblePlaybook credentialsId: 'deploy_server', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventories/dev/hosts', playbook: 'main.yml'
                            
            
            }
        }
    }
}
