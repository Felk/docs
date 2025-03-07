---
title: Changelog
excerpt: A summary of the latest changes to all Timescale products.
keywords: [changelog, upgrades, updates, releases]
---

# Changelog

All the latest features and updates to Timescale products.

## ⚡ Performance improvements for live migration to Timescale Cloud
<Label type="date">June 27, 2024</Label>

The following improvements have been made to the Timescale [live-migration docker image](https://hub.docker.com/r/timescale/live-migration/tags):

- Table-based filtering is now available during live migration.  
- Improvements to pbcopydb increase performance and remove unhelpful warning messages.
- The user notification log enables you to always select the most recent release for a migration run.

For improved stability and new features, update to the latest [timescale/live-migration](https://hub.docker.com/r/timescale/live-migration/tags) docker image. To learn more, see the [live migration docs](https://docs.timescale.com/migrate/latest/live-migration/).

## 🦙Ollama integration in pgai

<Label type="date">June 21, 2024</Label>

Ollama is now integrated with [pgai](https://github.com/timescale/pgai).

Ollama is the easiest and most popular way to get up and running with open-source 
language models. Think of Ollama as _Docker for LLMs_, enabling easy access and usage 
of a variety of open-source models like Llama 3, Mistral, Phi 3, Gemma, and more. 

With the pgai extension integrated in your database, embed Ollama AI into your app using
SQL. For example:

```sql
select ollama_generate
( 'llava:7b'
, 'Please describe this image.'
, _images=> array[pg_read_binary_file('/pgai/tests/postgresql-vs-pinecone.jpg')]
, _system=>'you are a helpful assistant'
, _options=> jsonb_build_object
  ( 'seed', 42
  , 'temperature', 0.9
  )
)->>'response'
;
```

To learn more, see the [pgai Ollama documentation](https://github.com/timescale/pgai/blob/main/docs/ollama.md).


## 🧙 Compression Wizard

<Label type="date">June 13, 2024</Label>

The compression wizard is now available on Timescale Cloud. Select a hypertable and be guided through enabling compression through the UI!

To access the compression wizard, navigate to `Explorer`, and select the hypertable you would like to compress. In the top right corner, hover where it says `Compression off`, and open the wizard. You will then be guided through the process of configuring compression for your hypertable, and can compress it directly through the UI.

![Run the compression wizard in Timescale Console](https://assets.timescale.com/docs/images/compress-data-in-console.png)

## 🏎️💨 High Performance AI Apps With pgvectorscale

<Label type="date">June 11, 2024</Label>

The [vectorscale extension][pgvectorscale] is now available on [Timescale Cloud][signup].

pgvectorscale complements pgvector, the open-source vector data extension for PostgreSQL, and introduces the
following key innovations for pgvector data:

- A new index type called StreamingDiskANN, inspired by the DiskANN algorithm, based on research from Microsoft.
- Statistical Binary Quantization: developed by Timescale researchers, This compression method improves on
  standard Binary Quantization.

On benchmark dataset of 50 million Cohere embeddings (768 dimensions each), PostgreSQL with pgvector and
pgvectorscale achieves 28x lower p95 latency and 16x higher query throughput compared to Pinecone's storage
optimized (s1) index for approximate nearest neighbor queries at 99% recall, all at 75% less cost when
self-hosted on AWS EC2.

To learn more, see the [pgvectorscale documentation][pgvectorscale].

## 🧐Integrate AI Into Your Database Using pgai

<Label type="date">June 11, 2024</Label>

The [pgai extension][pgai] is now available on [Timescale Cloud][signup].

pgai brings embedding and generation AI models closer to the database. With pgai, you can now do the following directly
from within PostgreSQL in a SQL query:

* Create embeddings for your data.
* Retrieve LLM chat completions from models like OpenAI GPT4o.
* Reason over your data and facilitate use cases like classification, summarization, and data enrichment on your existing relational data in PostgreSQL.

To learn more, see the [pgai documentation][pgai].

## 🐅Continuous Aggregate and Hypertable Improvements for TimescaleDB
<Label type="date">June 7, 2024</Label>

The 2.15.x releases contains performance improvements and bug fixes. Highlights in these releases are:

- Continuous Aggregate now supports `time_bucket` with origin and/or offset.
- Hypertable compression has the following improvements:
  - Recommend optimized defaults for segment by and order by when configuring compression through analysis of table configuration and statistics.
  - Added planner support to check more kinds of WHERE conditions before decompression.
    This reduces the number of rows that have to be decompressed.
  - You can now use minmax sparse indexes when you compress columns with btree indexes.
  - Vectorize filters in the WHERE clause that contain text equality operators and LIKE expressions.

To learn more, see the [TimescaleDB release notes](https://github.com/timescale/timescaledb/releases).

## 🔍 Database Audit Logging with pgaudit
<Label type="date">May 31, 2024</Label>

The [PostgreSQL Audit extension(pgaudit)](https://github.com/pgaudit/pgaudit/) is now available on [Timescale Cloud][signup].
pgaudit provides detailed database session and object audit logging in the Timescale
Cloud logs.

If you have strict security and compliance requirements and need to log all operations
on the database level, pgaudit can help. You can also export these audit logs to
[Amazon CloudWatch](https://aws.amazon.com/cloudwatch/).

To learn more, see the [pgaudit documentation](https://github.com/pgaudit/pgaudit/).

## 🌡 International System of Unit Support with postgresql-unit
<Label type="date">May 31, 2024</Label>

The [SI Units for PostgreSQL extension(unit)](https://github.com/df7cb/postgresql-unit) provides support for the
[ISU](https://en.wikipedia.org/wiki/International_System_of_Units) in [Timescale Cloud][signup].

You can use Timescale Cloud to solve day-to-day questions. For example, to see what 50°C is in °F, run the following
query in your Timescale Cloud service:

```
SELECT '50°C'::unit @ '°F' as temp;
  temp
--------
 122 °F
(1 row)
```

To learn more, see the [postgresql-unit documentation](https://github.com/df7cb/postgresql-unit).

[release-notes]: /about/:currentVersion:/release-notes/
[timescaledb-releases]: https://github.com/timescale/timescaledb/releases/
[pgai]: https://github.com/timescale/pgai
[pgvectorscale]: https://github.com/timescale/pgvectorscale/
[signup]: https://console.cloud.timescale.com/signup
