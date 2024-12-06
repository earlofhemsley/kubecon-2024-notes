# Object storage is all you need

Object storage is a de facto standard that has multiple implementations.

Non posix file system. Infinitely scalable.

## Attributes of object storage

### Performance characteristics

High latency (downside)
High parallelism
Dynamically scaled based on suage
High total throughput with sufficient parallelism

### Concurrent updates

The original usecase for cloud object storage was serving up web pages. There's not much concurrency problems there b/c the deployment pipeline is one and done.
Later use cases brought concurrency to the forefront. So, some solutions came up
- Content addressing 
- Signed URLs
- Using a DB (hacky)
- PUT with `If-None-Match: *`
    - "Write only if object not exists"
    - Now supported for S3, Cloudflare R2, others

Object storage doesn't work for everything
OCI storage registries came out of this also

### The Log

files can be created in numeric order: 0000, 0001, 0002, etc.
this effectively creates a log, which is the basic database primitive
you can build any data storage system, i.e., a db, from this.
[jay kreps article about the log](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)

## Things being built

yey toca

### Open table formats

Analytics dbs (snowflake, databricks, etc.) are built on object stores. They use open formats now (Delta Lake, Iceberg, Hudi). These are essentially [parquet files](https://parquet.apache.org/) of tables and updates to the and updates to a db schema. This effectively turns the object store into an immutable log where you can query data state at any point in time. (!)

### Virtual disks

[dis](https://github.com/asch/dis) local ssd cache, then send changed blocks to s3 as a log in batches. an in-memory cache is maintained that helps you know where current blocks can be found. `fsync` means "flush cache". implemented on the linux device mapper

### Leader election

[blog post](https://www.morling.dev/blog/leader-election-with-s3-conditional-writes/)

### Database

[SlateDB](https://github.com/slatedb) is sqlite backed by an object store. Early stage embedded db.

### Vector Database

[turbopuffer](https://www.morling.dev/blog/leader-election-with-s3-conditional-writes/) local ssd cache in front of s3 storage

### Kafka implementation

[WarpStream](https://www.warpstream.com/) ... kafka compatible data store. Cloud object stores replicate between AZs without paying for network costs. Higher latency than other kafka implementations, but cheap and easy to operate. Confluent (data streaming platform) bought them.

## Other things that might be built?

Future object stores will have lower latency

Lots of dbs / apps are built on top of object storage


