def userInput = true
def didTimeout = false
node {
     stage("Get State") {
            deleteDir()
            sh '''
            git clone ${GIT_URL}
            cd ./ct_node_basic/infrastructure
            aws s3 cp s3://${STACK}-${PROJECT_NAME}/state/terraform.tfstate terraform.tfstate  --region ${REGION}
            aws s3 cp  s3://${STACK}-${PROJECT_NAME}/state/terraform.tfstate.backup terraform.tfstate.backup --region ${REGION}
           '''
        }
        stage("Destroy Infrastructure") {
                    sh '''
                    cd ./ct_node_basic/infrastructure
                    terraform destroy -auto-approve
                   '''
                }
}