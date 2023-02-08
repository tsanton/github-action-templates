# **Docker-Compose Build** #

## **Variables** ##

See [action.yaml](./action.yaml) file for variable explanation.

## **Invocation** ##

```yaml
- name: Docker compose build
  uses: tsanton/github-action-templates/actions/docker-compose-build@main
  with:
    compose_file_name: docker-compose.yaml
    compose_file_path: ./
    additional_compose_build_files: |
      ./compose-files/docker-compose.build1-override.yaml
      ./compose-files/docker-compose.build2-override.yaml
```