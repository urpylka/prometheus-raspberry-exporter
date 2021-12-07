# Raspberry exporter

Export Raspberry Pi metrics in *Prometheus* *node_exporter*'s **textfile** format.

It can also be used with other ARM SOCs to simply export the *CPU* temperature.

## Dependencies

 * Prometheus (obviously)
 * Node Exporter with textfile collector

## Install

- copy `rpi_exporter` to `/usr/local/bin`.
- copy `rpi_exporter.service` to `/etc/systemd/system`
- enable and start `rpi_exporter`

For example you can deploy using git:

``` bash
cd /opt
sudo git clone https://github.com/prontog/prometheus-raspberry-exporter
cd prometheus-raspberry-exporter
sudo ln -s /opt/prometheus-raspberry-exporter/rpi_exporter.service /etc/systemd/system
sudo ln -s /opt/prometheus-raspberry-exporter/rpi_exporter /usr/local/bin
sudo systemctl enable rpi_exporter
sudo systemctl start rpi_exporter
```

## Configure your node exporter

Make sure your node exporter uses `textfile` in `--collectors.enabled` and add the following parameter: `--collector.textfile.directory=/var/lib/node_exporter`

## Example queries

```
rpi_temperature{job="node"}
rpi_freq{job="node",device="arm"}
rpi_volt{job="node",device="core"}
rpi_mem{job="node",device="arm"}
```
