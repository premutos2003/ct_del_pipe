def userInput = true
def didTimeout = false
node {
     stage("Get State") {
            deleteDir()

            sh '''
                export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY}
                        export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_KEY}
            git clone https://github.com/premutos2003/ct_node_basic.git
            cd ./ct_node_basic/infrastructure
            aws s3 cp s3://${STACK}-${PROJECT_NAME}/state/terraform.tfstate ./terraform.tfstate  --region ${REGION}
            aws s3 cp s3://${STACK}-${PROJECT_NAME}/state/terraform.tfstate.backup ./terraform.tfstate.backup --region ${REGION}
                                terraform destroy -auto-approve

           '''
        }

}