# Prometheus Raspberry Pi Exporter

Export Raspberry Pi metrics in Prometheus node_exporter's textfile format.

To visualizate it you can use preconfigured [Grafana dashboard](./grafana_dashboard.json).

![image](./grafana_dashboard.jpeg)

## Install

```bash
curl -o /usr/local/bin/rpi_exporter https://raw.githubusercontent.com/urpylka/prometheus-raspberry-exporter/master/rpi_exporter
curl -o /etc/systemd/system/rpi_exporter.service https://raw.githubusercontent.com/urpylka/prometheus-raspberry-exporter/master/rpi_exporter.service
chmod +x /usr/local/bin/rpi_exporter
sudo systemctl enable rpi_exporter
sudo systemctl start rpi_exporter
```

To uninstall use:

```bash
sudo systemctl stop rpi_exporter
sudo systemctl disable rpi_exporter
sudo rm /etc/systemd/system/rpi_exporter.service
sudo rm /usr/local/bin/rpi_exporter
```

## Configure your node exporter

1. Make sure your node exporter uses `textfile` in `--collectors.enabled`
2. Add the following parameter `--collector.textfile.directory=/var/lib/node_exporter`

## Example queries

```prom
rpi_temperature{chip="cpu-thermal",sensor="thermal_zone0"} 52.078
rpi_freq{device="arm"} 1400000000
rpi_freq{device="core"} 400000000
rpi_freq{device="h264"} 0
rpi_freq{device="isp"} 0
rpi_freq{device="v3d"} 300000000
rpi_freq{device="uart"} 48000000
rpi_freq{device="pwm"} 0
rpi_freq{device="emmc"} 200000000
rpi_freq{device="pixel"} 338000
rpi_freq{device="vec"} 108000000
rpi_freq{device="hdmi"} 0
rpi_freq{device="dpi"} 0
rpi_volt{device="core"} 1.3750
rpi_volt{device="sdram_c"} 1.2500
rpi_volt{device="sdram_i"} 1.2500
rpi_volt{device="sdram_p"} 1.2250
rpi_mem{device="arm"} 896
rpi_mem{device="gpu"} 128
rpi_throttled 19
```
