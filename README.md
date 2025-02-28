# azure-pipeline-templates

A collection of common Azure Pipeline tasks to be used across out projects

## Usage

Templates are meant to be included into a project pipeline. Please refer to [this guide](https://github.com/MicrosoftDocs/azure-devops-docs/blob/master/docs/pipelines/process/templates.md#use-other-repositories) for examples.

### Best practices

- Always include templates in your pipeline specifying the reference tag, so a new template version can never break your CI/CD workflow.
- When writing templates, make little-to-no use of default values. Instead, pretend the host pipeline to provide them.

## Available templates

- [Rest Healthcheck](templates/rest-healthcheck)
- [Node Github Release](templates/node-github-release)
- [Maven Github Release](templates/maven-github-release)
- [Autogenerated Client SDK Publish](templates/client-sdk-publish)
- [Node Job Setup template](templates/node-job-setup)
- [Terraform Setup](templates/terraform-setup)
- [Terraform Install Azure RM Custom Provider](templates/terraform-custom-azurerm)

## Contributing

### Create a new template

- Create a dedicated folder in `/templates`, with the name of the template.
- Please remember that templates are not inheritedly bound to any specific project or tech: if the template works only on a specific context, make it explicit (example: prefer `npm-publish` to `publish` when writing a template to publish a module on npm).
- In the folder create a `yaml` file (naming isn't really important, you can call it `index.yaml` or `template.yaml`).
- In the same folder add a specific README file with:
  - a brief description of the template
  - an example snippet to describe usage
  - a full parameters table
- Add an entry in the `Available templates` section of the repo main README (this file), with a link to the README of the template you just created.

### Testing

We have a [pipeline](.devops/test-pipelines.yaml) configured on this project to run test against the templates we produce. Although Azure Pipelines' DSL is not designed for a test-first approach, it's worth to try. Assets, mocks and scripts used for testings can be placed in [`.devops/__tests__`](.devops/__tests__) folder.

Tests are configured to run on every Pull Request and there's no way ton run tests locally, so far. To use a _red-green-refactor_ approach, the best we can do is to work on a branch and open a draft PR on that.

### Release a new version

New versions are created automatically on each merge on master branch. In the need of creating a release manually, use the pipeline [`azure-pipeline-templates.release`](https://dev.azure.com/pagopa-io/azure-pipeline-templates/_build?definitionId=134)
