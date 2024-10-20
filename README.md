# pi-hole-deployment

## prepare infrastructure

### infra stack

- Hardware: Raspberry Pi 3
- OS: Raspberry Pi OS Lite (64-bit)
- Wi-Fi dongle

### OS

- Configure IP address in `/etc/network/interfaces`
example:

```bash
# static IP on wlan0
allow-hotplug wlan0
iface wlan0 inet static
  wpa-ssid "<Wi-Fi SSID>"
  wpa-psk "<Wi-Fi pass>"
  address <static IP> # e.g 10.0.4.123
  netmask <netmask> # e.g 255.255.255.0
  gateway <gateway> # e.g 10.0.4.1

# disable DHCP for wlan1
allow-hotplug wlan1
iface wlan1 inet manual
```

- Install docker `curl -sSL https://get.docker.com | sh`

## Pi-hole

### Pi-hole stack

- Pi-hole
- Pi-hole Prometheus Exporter
- Prometheus Node Exporter

### Pi-hole deployment

For the Pi-hole app itself:

1. Run the installation script provided [here](https://docs.pi-hole.net/main/basic-install/)

In `/pi-hole-server`:

1. Update `pihole-api-token.txt` with the Pi-hole API token.
1. Replace `PIHOLE_HOSTNAME` value in `docker-compose.yaml`
1. Run `docker compose up` to simplify visualizing logs. Ensure all containers
   are running and that there are no errors
1. Run `docker compose up -d` to run the containers long term in detached mode.

In `/node-exporter`:

1. Run `docker compose up` to simplify visualizing logs. Ensure all containers
   are running and that there are no errors
1. Run `docker compose up -d` to run the containers long term in detached mode.

## monitoring

### monitoring stack

- Prometheus
- Grafana
- Prometheus Node Exporter

### monitoring deployment

In `/monitoring-server`

1. Run `docker compose up` to simplify visualizing logs. Ensure all containers
   are running and that there are no errors
1. Run `docker compose up -d` to run the containers long term in detached mode.
1. In Grafana add our Prometheus deployment as a data source.
1. In Grafana import dashboard JSON from [here](https://github.com/eko/pihole-exporter)

In `/node-exporter`:

1. Run `docker compose up` to simplify visualizing logs. Ensure all containers
   are running and that there are no errors
1. Run `docker compose up -d` to run the containers long term in detached mode.
