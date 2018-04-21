def userInput = true
def didTimeout = false
node {
     stage("Delete Infrastructure") {
            deleteDir()

            sh '''
                export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY}
                        export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_KEY}

            str=$(curl -v -sS 'docker.for.mac.localhost:3000/app_infra' | jq -r '.[0]')
            instance_id=$(echo $str | jq -r '.app_instance_id')

            aws ec2 terminate-instances --instance-ids $instance_id

            git clone https://github.com/premutos2003/ct_node_basic.git
            cd ./ct_node_basic/infrastructure
            aws s3 cp s3://${STACK}-${PROJECT_NAME}/state/terraform.tfstate ./terraform.tfstate  --region ${REGION}
            terraform init
            terraform destroy -force  --target=aws_iam_instance_profile.deploy_profile --target=aws_iam_role.deploy_role --target=aws_iam_policy.deploy_policy --target=aws_s3_bucket.s3_bucket_deploy_artefact -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY}

            cd ..
            cd ./key
            terraform  destroy -force -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY}
           '''
        }

}