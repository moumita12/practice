
node('linux') {
    git url: 'https://github.com/moumita12/practice.git',branch: 'master'
    stage('Test') {
        sh "env"          
    }
    
    stage ("GetInstances") {

                                            sh "aws ec2 describe-instances --region us-east-1"
                                        }

                stage ("CreateInstance") {
                                           output = sh returnStdout: true, script: 'aws ec2 run-instances --image-id ami-013be31976ca2c322 --count 1 --instance-type t2.micro --key-name mou1key --security-group-ids sg-0ae4d2d25ab0ba7d8 --subnet-id subnet-0fef304de7b675c3d --region us-east-1 | jq .Instances[0].InstanceId'
                                           echo "${output}"
                                           sh "aws ec2 wait instance-running --region us-east-1 --instance-ids ${output}"
                                         }
                stage ("TerminateInstance") {
                                          sh "aws ec2 stop-instances --region us-east-1 --instance-ids ${output}"  
                                          
                                         }
                                         
                                        
}
