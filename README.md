# spark-history-server-config

## Spark History Server Configuration Options

| Property Name                                 | Default                             | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------------------------------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `spark.history.fs.cleaner.enabled`            | false                               | Specifies whether the History Server should periodically clean up event logs from storage.                                                                                                                                                                                                                                                                                                                                                                                                     |
| `spark.history.fs.cleaner.interval`           | 1d                                  | When `spark.history.fs.cleaner.enabled=true`, specifies how often the filesystem job history cleaner checks for files to delete. Files are deleted if at least one of two conditions holds. First, they're deleted if they're older than `spark.history.fs.cleaner.maxAge`. They are also deleted if the number of files is more than `spark.history.fs.cleaner.maxNum`, Spark tries to clean up the completed attempts from the applications based on the order of their oldest attempt time. |
| `spark.history.fs.cleaner.maxAge`             | 7d                                  | When `spark.history.fs.cleaner.enabled=true`, job history files older than this will be deleted when the filesystem history cleaner runs.                                                                                                                                                                                                                                                                                                                                                      |
| `spark.history.fs.driverlog.cleaner.interval` | `spark.history.fs.cleaner.interval` | When `spark.history.fs.driverlog.cleaner.enabled=true`, specifies how often the filesystem driver log cleaner checks for files to delete. Files are only deleted if they are older than `spark.history.fs.driverlog.cleaner.maxAge`                                                                                                                                                                                                                                                            |
| `spark.history.fs.driverlog.cleaner.maxAge`   | `spark.history.fs.cleaner.maxAge`   | When `spark.history.fs.driverlog.cleaner.enabled=true`, driver log files older than this will be deleted when the driver log cleaner runs.                                                                                                                                                                                                                                                                                                                                                     |

## Setting the configuration via Helm `values.yaml`

```yaml
...

image:
  repository: lightbend/spark-history-server
  tag: 2.4.0
  pullPolicy: IfNotPresent

environment:
  SPARK_HISTORY_OPTS: "-Dspark.history.fs.cleaner.enabled=true -Dspark.history.fs.cleaner.maxAge=7d"

imagePullSecrets: []

...
```
