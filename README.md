# jenkins-it
Jenkins instance for IT purposes

# Overiew
This project contains several pipelines that invoke various SaaS api endpoints. It also contains a jenkins.yaml configuration that defines all the pipelines. 
This project is designed to work in conjuction with the following projects to deploy required infrastructure to AWS via terraform.
    https://github.com/nabilhq/terraform-modules/tree/main/jenkins-api-gateway
    https://github.com/nabilhq/terraform-modules/tree/main/jenkins

# Dependecies
    AWS
        EC2: Runs the master jenkins instance.
        Secrets Manager: Used to store API tokens and other secrets used by jenkins.
        API Gateway: Used to receive and proxy github webhook events to a Lambda. 
            Refer to https://github.com/nabilhq/terraform-modules/tree/main/jenkins-api-gateway for config.
        Lambda: Used to forward github event webhooks to jenkins. 
            Refer to https://github.com/nabilhq/terraform-modules/tree/main/jenkins-api-gateway for config.
        IAM: Used to grant the Jnekins Ec2 access to Secrets Manager and S3
        S3: Used to store lambda packages
        Load Balancer: Used to terminate the SSL certficate and forward traffic to the Jenkins EC2 instance.
        Route53: Used for the DNS alias to forward traffic the ALB.
    GitHub
    Idp Provider
        This instance is configured to use SAML for authentication.