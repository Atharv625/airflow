 .. Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

 ..   http://www.apache.org/licenses/LICENSE-2.0

 .. Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

.. _howto/operator:S3ToSnowflakeOperator:

CopyFromExternalStageToSnowflakeOperator
========================================

Use the :class:`CopyFromExternalStageToSnowflakeOperator <airflow.providers.snowflake.transfers.copy_into_snowflake>`
to load data stored in `AWS S3 <https://aws.amazon.com/s3/>`__,
`Google Cloud Storage <https://cloud.google.com/storage>`__, or
`Azure Blob Storage <https://azure.microsoft.com/products/storage/blobs>`__ to a Snowflake table.

.. note:: This operator is a simple wrapper in top of
    `COPY INTO table <https://docs.snowflake.com/en/sql-reference/sql/copy-into-table#>`__ query, and
    required `creating stage <https://docs.snowflake.com/en/sql-reference/sql/create-stage>`__ first.

Using the Operator
^^^^^^^^^^^^^^^^^^

Similarly to the :class:`SnowflakeOperator <airflow.providers.snowflake.operators.snowflake>`, use the ``snowflake_conn_id`` and
the additional relevant parameters to establish connection with your Snowflake instance.
This operator will allow loading of one or more named files from a specific Snowflake stage (predefined S3 path). In order to do so
pass the relevant file names to the ``files`` parameter and the relevant Snowflake stage to the ``stage`` parameter.
``pattern`` can be used to specify the file names and/or paths match patterns
(see `docs <https://docs.snowflake.com/en/sql-reference/sql/copy-into-table.html#loading-using-pattern-matching>`__).
``file_format`` can be used to either reference an already existing Snowflake file format or a custom string that defines
a file format (see `docs <https://docs.snowflake.com/en/sql-reference/sql/create-file-format.html>`__).

An example usage of the CopyFromExternalStageToSnowflakeOperator is as follows:

.. exampleinclude:: /../../snowflake/tests/system/snowflake/example_copy_into_snowflake.py
    :language: python
    :start-after: [START howto_operator_s3_copy_into_snowflake]
    :end-before: [END howto_operator_s3_copy_into_snowflake]
    :dedent: 4
