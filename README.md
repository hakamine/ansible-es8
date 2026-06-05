# internal-es8-el9 (Elasticsearch role)

<!--TOC-->

______________________________________________________________________

- [1. Required variables](#1-required-variables)
- [2. Optional variables](#2-optional-variables)
- [3. Example config](#3-example-config)

______________________________________________________________________

<!--TOC-->

This role installs Elasticsearch 8.x. Main features:

- It is intended to be used instead of
the role <https://github.com/artefactual-labs/ansible-elasticsearch>
(in order to prevent obsolete/unrequired changes carried from previous
versions)
- Based on installation procedure at
  <https://www.elastic.co/guide/en/elasticsearch/reference/8.19/rpm.html> and
  <https://www.elastic.co/guide/en/elasticsearch/reference/8.19/deb.html>
- As Elasticsearch 8.x includes a bundled JVM supported by Elastic,
there is no need to install Java/OpenJDK separately (ref.
  <https://www.elastic.co/support/matrix#matrix_jvm> )
- Elasticsearch 8.x by default has security enabled. This role changes
the configuration to disable security, so that Archivematica can use it
- Heap size is configured in `/etc/elasticsearch/jvm.options.d/`
- ES_TMPDIR env var configured in `/etc/sysconfig/elasticsearch` (RedHat) 
  or `/etc/sysconfig/elasticsearch` (Debian)
## 1. Required variables

Define in host_vars/group_vars:

- `es_version`: version of the ES package

## 2. Optional variables

The following are optional. If not defined, ES will use package
installation defaults. Recommended to be defined for use with
Archivematica:

- `es_tmpdir`: temporary directory name (assigned to ES_TMPDIR env var)
  (default: undefined)

- `es_tmpdir_create`: whether or not create the temporary directory specified
  in `es_tmpdir`
  (default: undefined)

- `es_heap_size`
- `es_cfg_cluster_name`
- `es_cfg_bootstrap_memory_lock`
- `es_cfg_http_max_content_length`
- `es_cfg_discovery_type`

## 3. Example config

```yaml
es_version: 8.19.15
es_tmpdir: /var/lib/elasticsearch/tmp
es_tmpdir_create: true
es_heap_size: 1g
es_cfg_cluster_name: mycluster
es_cfg_bootstrap_memory_lock: true
es_cfg_http_max_content_length: 1024mb
es_cfg_discovery_type: single-node
```
