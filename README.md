# Rust Implementation of a PuppetDB CLI

[![Build status](https://ci.appveyor.com/api/projects/status/bhln68k6pdfixrun?svg=true)](https://ci.appveyor.com/project/ajroetker/rust-puppetdb-cli)
[![Build Status](https://travis-ci.org/ajroetker/rust-puppetdb-cli.svg)](https://travis-ci.org/ajroetker/rust-puppetdb-cli)
[![Crates.io](https://img.shields.io/crates/v/rust-puppetdb-cli.svg)](https://crates.io/crates/rust-puppetdb-cli)

## Compatibility

This CLI is compatible with PuppetDB v4.

## Installation

Using `rustc` and `cargo` (stable, beta, or nightly):

```zsh
<rust-puppetdb-cli>$ export PATH=./target/debug
<rust-puppetdb-cli>$ cargo build
<rust-puppetdb-cli>$ puppet-query 'nodes[certname]{}'
[
  {
    "certname" : "baz.example.com"
  },
  {
    "certname" : "bar.example.com"
  },
  {
    "certname" : "foo.example.com"
  }
]
<rust-puppetdb-cli>$ puppet-db status
{
  "puppetdb-status": {
    "service_version": "4.0.0-SNAPSHOT",
    "service_status_version": 1,
    "detail_level": "info",
    "state": "running",
    "status": {
      "maintenance_mode?": false,
      "queue_depth": 0,
      "read_db_up?": true,
      "write_db_up?": true
    }
  },
  "status-service": {
    "service_version": "0.3.1",
    "service_status_version": 1,
    "detail_level": "info",
    "state": "running",
    "status": {}
  }
}
```

## Configuration

The Rust PuppetDB CLI accepts a `--config=<path_to_config>` flag which allows
you to configure your ssl credentials and the location of your PuppetDB.

By default the tool will use `$HOME/.puppetlabs/client-tools/puppetdb.conf` as it's
configuration file if it exists.

The format of the config file can be deduced from the following example.

```json
  {
    "puppetdb" : {
      "server_urls" : [
        "https://pdb.internal.lan:8081",
        "https://read-pdb.internal.lan:8081"
      ],
      "cacert" : "/path/to/cacert",
      "cert" : "/path/to/cert",
      "key" : "/path/to/private_key"
      },
    }
  }
```

## TODO

- [ ] Add failover for `server_urls`
- [ ] Add `--log-level` and `--silent` options
- [ ] Add testing for all the things
