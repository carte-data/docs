# Connections

This page lists all the available connections in Carte. These connections are supported natively, meaning they can be configured from the extract config YAML. You can also use any Extractor available in the Amundsen Databuilder library, since Carte is compatible with it. For this see [the relevant page](/reference/databuilder).

| Connector   | Extracts tables vs views | Extracts enum values              | Extracts location |
| ----------- | ------------------------ | --------------------------------- | ----------------- |
| AWS Glue    | :material-check:         | :material-close: No enums in Glue | :material-check:  |
| PostgreSQL  | :material-check:         | :material-close:                  | :material-check:  |
| JSON Schema | :material-close:         | :material-check:                  | :material-check:  |

## AWS Glue

The Glue connector pulls down the AWS Glue data catalog, with all its databases and tables.
The AWS Glue connector just needs a name for the connection and nothing else. It needs AWS credentials to be configured on your system, using the AWS CLI or just by having the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables set. Specifying the access key and secret in the YAML configuration is insecure (since this file is supposed to be committed to Git) and is not supported currently.

Example config:

```yaml
connections:
  - type: glue
    name: aws_glue
```

This connector also extracts the S3 location of a table if it exists.

## PostgreSQL

The Postgres connector extracts all tables from the specified database. It has the following options:

`included schemas`: By default, only tables under the `public` schema are extracted. This means that you avoid extracting internal Postgres tables, which is what you probably want most of the time. However, by setting this option to an array of strings, you can manually specify the schemas to extract.

`connection_string`: The connection string with details on how to reach the database. It has the following format:

  `postgresql://<user>:<password>@<host>:<port>/<database>`

Embedding your database password in your config is not ideal, and I'm working on a solution to avoid this.

Example config:

```yaml
connections:
  - type: postgresql
    config:
      connection_string: ...
      included_schemas:
        - public
```

The name of the connection will be postgres.

## JSON Schema

Carte is able to extract metadata from a JSON schema, which is useful if your connection is not supported, or if you're generating your schema.
Since JSON schemas can be very complex, this connector currently supports a limited set of use cases (that we needed at Shapr3D).

### Required config options

`database`: The database to put extracted metadata into

`schema_path`: The path to the JSON schema. This can be a local relative path, or an S3 URI, which must start with `s3://`

### Optional config:

`object_expand`: this is a list of strings, specifying which objects to expand. This means that the subproperties of this column will be unnested and listed in the metadata descriptor with a `<column>.<subcolumn>` format. For this to work, the specified JSON schema property has to be of type `object` and has to have nested `properties`.

`pivot_column`: This option splits the schema into multiple datasets based on the value of a `const` within a `oneOf`. Example schema:

```json
{
    "oneOf":
        [{
            "properties": {
                "vehicle_type": {
                    "const": "boat"
                },
                ...
            }
        }, {
            "properties": {
                "vehicle_type": {
                    "const": "car"
                },
                "brand": {
                    "type": "Honda"
                }
                ...
            }
        }]
}
```

If you specify a `pivot_column` of `vehicle_type` here, you'll get two datasets extracted, one with name `boat`, the other named `car`. The car dataset will also have a `brand` column.
In short, this option splits the schema into as many datasets as options in a top-level `oneOf` construct, and the pivot column tells Carte which one to use as name. Then each of these will get merged into the root schema, so you'll get a separate dataset for each constraint with different properties, but each one will also have the root properties. This option can also be combined with the `object_expand` config.
