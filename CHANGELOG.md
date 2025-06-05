# Changelog

## 1.3.0.1 (FORK)
- enable_phone_call_tracking: False
- Database name: influxdb-telegraf
- Phone Call Tracking Panels removed in Grafana for InfluxDB v1 datasource
- Cache Use Patch from https://github.com/Ragin-LundF/telegraf_fritzbox_monitor/commit/6dd68aaa53c951f0a84732d7ee1adac6309631bc



## 1.3.0
Support for InfluxDB 2.x

- Added a new Grafana Dashboard Template [GrafanaFritzBoxDashboard_Influx2.json](GrafanaFritzBoxDashboard_Influx2.json)

Update of dependencies

- `fritzconnection` to 1.12.0
- `PyYAML` 6.0.0 replaces now HiYaPyCo (thanks to @sbstnzmr)

It is required to re-execute the pip installer:

```bash
pip3 install -r requirements.txt
./install.sh
```

The `install.sh` script will only update the python files, but not an existing configuration (neither telegraf nor `config.yaml`).

## 1.2.0

Please ensure, that the directory of the application has the same user/group as the telegraf daemon.
By default, the `install.sh` will set the owner to `telegraf:telegraf`.

It is required to re-execute the pip installer:

```bash
pip3 install -r requirements.txt
```

### Phone Call Counter
Added a feature to see how many calls are
- missed
- incoming
- outgoing

In addition, the total time spent on these call types is also counted.

This feature uses a local SQLite database to store the calls and to avoid duplicates while a day.
It stores some data there, to allow more statistics later.
The data will also be cleaned up after some days to avoid too much redundant data.
In the YAML configuration file, it is possible to configure this feature. 

To see the phone call visualization in Grafana, please update your Dashboard configuration with the current version.

### YAML configuration possibility
With this release, it is possible to configure most parameters via a YAML configuration file.
The only parameter, which still has to be used via CLI is the address `-i` parameter.

Arguments from the CLI will always overwrite this config.

To have full separation between default config and custom config and to not overwrite something, a custom configuration should be written in a file called `config_custom.yaml`.
The configuration of this file will be merged with the default `config.yaml` file.

For more information about this feature, please look into the `README.md`.

### install.sh optimization
The `install.sh` file will no longer overwrite the `telegraf_fritzbox.conf` file in `/etc/telegraf/telegraf.d/`` 
