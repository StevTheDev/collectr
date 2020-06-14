# Collectr, a log collection tool written in Rust

A project inspired by [fluentd](github.com/fluent/fluentd), `collectr` watches files and sends their contents elsewhere.

This is a hobby project - I want to accomplish some set of features, but probably won't cover everything. I want this to be an open project -  participation is welcome, as well as honest feedback.

To summarize `collectr`'s goals so far:

**Input**:
- Take a glob match, or list of glob matches, of file paths as arguments
- Follow each file independently

**Filter**:
- Convenient & arbitrary metadata tagging
    - System Environment
    - Configurable Key:Value Pairs
- Pattern or Tag Matching
    -  Metrics
- Handle Multi-line Messages

**Output**:
- `stdout`
- [prometheus](https://prometheus.io/docs/concepts/data_model/)
- [elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-your-data.html)
- [kafka](https://kafka.apache.org/10/javadoc/org/apache/kafka/clients/producer/KafkaProducer.html)
- [loki](https://grafana.com/oss/loki/)

That's right, `collectr` aims to interface well with Elasticsearch, Apache Kafka, Grafana Loki, and produce Prometheus metrics right out of the box.

## Configuration File Syntax

`collectr` hopes to have an easy to read, and easy to comprehend configuration file syntax. `collectr` is given a sires of input `jobs`, each of which is responsible for watching a set of files. Each `input` can be filtered and routed to a routed to a specific `output` and/or prometheus metric. 

```
---
input:
  job_1:
    file_1:
    - path: "/myfile"
      position: "/var/collectr/read.pos"
      patterns: []
        # actions: []
        # actions are metric or output selection
      outputs: []
        # - output_1
        # - output_2
    file_2:
      ...
  job_2:
    ...
output:
  output_1:
    ...
  output_2"
    ...
...

```

Participation and Feedback are encouraged for this project. Please [Join our Discord](https://discord.gg/WvWHPx) or share your ideas by [email](collectr@wh0.io)!
