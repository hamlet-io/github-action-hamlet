# hamlet-go Docker Action

This action allows you to easily run Hamlet Tasks.

# Supported Tasks

Currently supported tasks are:

* Read project.properties file into GITHUB_ENV persistent env file
* Generate Hamlet Schemas


## Inputs

### `task_build_schemas`

**Description** Generates Hamlet schemas such as the Component, ReferenceData and Metaparameter schemas
**Type** boolean
**Default** false

### `task_build_schemas_output`

**Description** Directory within the container to output the schemas. Defaults to the workspace root mounted inside the container at `/home/hamlet/src`
**Type** string
**Default** /github/workspace

## Example Usage

```yaml
uses: hamlet-io/github-action-hamlet@v1
with:
  task_build_schemas: true
  task_build_schemas_output: /home/hamlet/src/path/to/project/schema/directory
```

### `properties_file_path`

**Description** Path to a properties file containing environment variables. Only required to be specified if this Action is running against a Hamlet CMDB repository and the properties file path is not in the conventional location (pipelines/properties/<project>.properties).
**Type** string
**Default** ""

**Note:** A properties file will always be loaded into GITHUB_ENV if found, however the action that creates or updates GITHUB_ENV does not have access to the new value itself. To ensure access to a complete set of environment variables, a Job should begin with a stand-alone Action call used to establish them.

## Example Usage

```yaml
# with properties file in conventional location
uses: hamlet-io/github-action-hamlet@v1

# OR

# with properties file elsewhere
uses: hamlet-io/github-action-hamlet@v1
with:
  properties_file_path: ${{ github.workspace }}/path/project.properties
```

# Development

When updating this Action, committing the changes are not sufficient. You must tag your changes and push the tag, either overwriting the existing tag or pushing the new one.

```bash
# add tag
git tag <tag>

# push
git push <remote> <tag> # with --force to override

```