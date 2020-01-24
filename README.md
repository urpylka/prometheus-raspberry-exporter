# Raspberry exporter

Export Raspberry Pi metrics in *Prometheus* *node_exporter*'s **textfile** format.

It can also be used with other ARM SOCs to simply export the *CPU* temperature.

## Dependencies

 * Prometheus (obviously)
 * Node Exporter with textfile collector

## Install

- copy `raspberry_exporter` to `/usr/local/bin`.
- copy the systemd unit files to `/etc/systemd/system`
- enable and start `prometheus-raspberry-exporter.timer`

For example you can deploy using git:

``` bash
cd /opt
sudo git clone https://github.com/prontog/prometheus-raspberry-exporter
cd prometheus-raspberry-exporter
sudo ln -s /opt/prometheus-raspberry-exporter/prometheus-raspberry-exporter* /etc/systemd/system
sudo ln -s /opt/prometheus-raspberry-exporter/raspberry_exporter /usr/local/bin
sudo systemctl enable prometheus-raspberry-exporter.timer
sudo systemctl start prometheus-raspberry-exporter.timer
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
