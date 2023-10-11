# NSG&B Open API descriptions

This is a test for publishing NSG&B Open API descriptions in Github using [Redocly CLI](https://redocly.com/docs/cli/). See latest version of the published API documentation [here](https://nordicsmartgovernment.github.io/Nordic-Smart-Government-OpenAPI-Specifications/).

## Developing Open API description

### Install

1. Install [Node JS](https://nodejs.org/).
2. Clone this repo and run `npm install` in the repo root.
3. (OPTIONAL) Install redocly `npm i -g @redocly/cli@latest` for linting & other commands.

### Usage

#### `npm run preview`
Starts the reference docs preview server.

#### `npm run publish-v1`
Published the versioned API. Use v2 for the next version etc.

#### `npm run lint-v1`
Run API linter for the given version

## Contribution Guide

### Schemas

1. Navigate to the `openapi/components/schemas` folder.
2. Add a file named as you wish to name the schema.
3. Define the schema.
4. Refer to the schema using the `$ref` (see example below).

```yaml
  registeredAddress:
    $ref: './Address.yaml'
```

### Paths

#### Adding a Path

1. Navigate to the `openapi/paths` folder.
2. Add a new YAML file named like your URL endpoint except replacing `/` with `_` (or whichever character you prefer) and putting path parameters into curly braces like `{example}`.
3. Add the path and a ref to it inside of your `openapi.yaml` file inside of the `openapi` folder.

Example addition to the `openapi.yaml` file:
```yaml
'/customers/{id}':
  $ref: './paths/customers_{id}.yaml'
```

### Code samples

Automated code sample generations is enabled in the Redocly configuration file. Add manual code samples by the following process:

1. Navigate to the `openapi/code_samples` folder.
2. Navigate to the `<language>` (e.g. PHP) sub-folder.
3. Navigate to the `path` folder, and add ref to the code sample.

You can add languages by adding new folders at the appropriate path level.

More details inside the `code_samples` folder README.

## Publishing API versions

API versioning is done by creating a new API page for each version and publishing the bundled specification for that version. To create a new major version look into packages.json for example.

To bundle and publish new minor version use existing shorthands from packages.json, for example:
```
npm run publish-v2
```

Remember to update minor version number to API root in `openapi/v{number}.yaml`

### Add code examples

Test this library for code snippets:

* https://github.com/cdwv/oas3-api-snippet-enricher/

### Other useful commands

Preview any Open API spec:
```
redocly preview-docs bundled.yaml
```

Lint any Open API spec:
```
redocly lint bundled.yaml
```

Split Open API to redoc style directories:
```
redocly split bundled.yaml --outDir .
```

For more commands see [Redocly docs](https://redocly.com/docs/cli/commands/).
