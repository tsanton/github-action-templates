# **Docker-Compose Push Action** #

## **Variables** ##

See [action.yaml](./action.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Configure AWS Credentials
  uses: tsanton/github-action-templates/actions/configure-aws-credentials-1@main
  with:
    role-to-assume: arn:aws:iam::<aws-account-id>:role/<aws-iam-role-name>
    aws-region: eu-west-1

- name: Login to Amazon ECR
  id: login-ecr
  uses: aws-actions/amazon-ecr-login@v1

- name: Docker compose push
  uses: tsanton/github-action-templates/actions/docker-compose-push@main
  with:
    compose_file_path: application/
    compose_file_name: docker-compose.yaml
    tags: |
      latest
      ${{ github.run_number }}
```