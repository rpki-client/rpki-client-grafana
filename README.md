# Grafana dashboards for rpki-client

Dashboard templates for rpki-client using the new OpenMetrics output support by `rpki-client -m`.
The metrics file needs to be either added as a textfile collector in `node_exporter` or it is
served by a webserver so prometheus can ingest it.

The overview dashboard shows some global stats and per _Trust Anchor Locator (TAL)_ information.
The _CA_ repository dashboard show per _Certification Authority (CA)_ information.

## node_exporter setup

The easiest way to serve the metrics file is by using `node_exporter` with `--collector.textfile.directory=/var/node_exporter`.
Just symlink the metrics file (default `/var/db/rpki-client/metrics`) into that directory as `rpki-client.prom`.

```
mkdir /var/node_exporter
cd /var/node_exporter
ln -s /var/db/rpki-client/metrics rpki-client.prom
```

rpki-client replaces the file after a successful run with an atomic rename(2). So `node_exporter` will never read a partial file.

## example overview panel

![example overview panel](/assets/rpki_overview.png)

## example CA panel

![example CA panel](/assets/rpki_ca_view.png)

