# Cadl APIView Emitter

This package provides the [Cadl](https://github.com/microsoft/cadl) emitter to produce APIView token file output from Cadl source.

## Install

Add `@azure-tools/cadl-apiview` to your `package.json` and run `npm install`.

## Emit APIView spec

1. Via the command line

```bash
cadl compile {path to cadl project} --emit=@azure-tools/cadl-apiview
```

2. Via the config

Add the following to the `cadl-project.yaml` file.

```yaml
emitters:
  @azure-tools/cadl-apiview: true
```

For configuration [see options](#emitter-options)

## Create API View

1. Log in to the API View site (apiview.dev)[https://apiview.dev].
2. Click the blue "Create Review" button in the bottom-right corner of the screen.
3. In the first block, load the token file generated by the `cadl-apiview` emitter.

## Revise API View

1. Log in to the API View site (apiview.dev)[https://apiview.dev].
2. Navigate to your review.
3. Click the "Revisions" tab in the top left.
4. Click the blue "Add Revision" button in the bottom-right corner of the screen.
5. In the first block, load the token file generated by the `cadl-apiview` emitter.

## Use APIView-specific decorators:

Currently there are no APIView-specific decorators...

## Emitter options:

Emitter options can be configured via the `cadl-project.yaml` configuration:

```yaml
emitters:
  '@azure-tools/cadl-apiview':
    <optionName>: <value>


# For example
emitters:
  '@azure-tools/cadl-apiview':
    output-file: my-custom-apiview.json
```

or via the command line with

```bash
--option "@azure-tools/cadl-apiview.<optionName>=<value>"

# For example
--option "@azure-tools/cadl-apiview.output-file=my-custom-apiview.json"
```

### `emitter-output-dir`

Configure the name of the output directory. Default is `cadl-output/@azure-tools/cadl-apiview`.

### `include-global-namespace`

Normally, APIView will filter all namespaces and only output those in the service namespace and any
subnamespaces. This is to filter out types that come from the Cadl compiler and supporting libraries.
This setting, if `true`, tells APIView to output the contents of the global (empty) namespace, which
would normally be excluded.

### `service`

Filter output to a single service definition. If omitted, all service defintions will be
output as separate APIView token files.

### `output-file`

Configure the name of the output JSON token file relative to the `output-dir`. For multi-service
specs, this option cannot be supplied unless the `service` option is also set. If outputting
all services in a multi-service spec, the output filename will be the service root namespace with the
`-apiview.json` suffix. Otherwise, the default is `apiview.json`.

### `version`

For multi-versioned Cadl specs, this parameter is used to control which version to emit. This
is not required for single-version specs. For multi-versioned specs, the unprojected Cadl will
be rendered if this is not supplied. For multi-service specs, this option cannot be supplied
unless the `service` option is also set.

## See also

- [Cadl Getting Started](https://github.com/microsoft/cadl#getting-started)
- [Cadl Tutorial](https://github.com/microsoft/cadl/blob/main/docs/tutorial.md)
- [Cadl for the OpenAPI Developer](https://github.com/microsoft/cadl/blob/main/docs/cadl-for-openapi-dev.md)
