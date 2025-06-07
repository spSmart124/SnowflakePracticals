# Stage And Ingestion
## Stage
Stage is a location in Snowflake from which data can be ingested into a Snowflake table. It is of two types.
1. External Stage
2. Internal Stage

### External Stage
External stage references external location that is not managed or billed by Snowflake. Example AWS S3, GCP, Azure etc. Here is the syntax to create and external stage.

#### Syntax
CREATE OR REPLACE STAGE <database>.<schema>.<stage_name>
url = '<external_url>'
file_format = <file_format>;

#### Example
CREATE OR REPLACE STAGE tasty_bytes.public.s3load
url = 's3://sfquickstarts/frostbyte_tastybytes/'
file_format = 'csv';

### Internal Stage
Internal stage does not have any external reference. It is managed and billed by Snowflake.

#### Syntax
CREATE OR REPLACE STAGE <database>.<schema>.<stage_name>;

#### Example
CREATE OR REPLACE STAGE tasty_bytes.public.tasty_bytes_internal_stage;

#### Types
* User stage - Can only be used by that specific user. Cannot be dropped.
* Table stage - Can only be used with the associated table. Cannot be dropped.
* Named stage - Can be used by multiple users and associated with multiple tables.

## Ingestion
You can easily ingest data into snowflake tables using "COPY INTO" command. It is a simple yet powerful command to quickly ingest the data into snowflake table.

#### Syntax
COPY INTO <database>.<schema>.<table_name> FROM @<database>.<schema>.<stage_name>/<path>;

#### Example
COPY INTO tasty_bytes.raw_pos.order_header
FROM @tasty_bytes.public.s3load/raw_pos/order_header/;

### Sample query
[Stage and Ingestion Queries](./stage_ingestion.sql)