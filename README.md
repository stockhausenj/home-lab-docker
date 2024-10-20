# pi-hole-deployment

## monitoring

### stack

- Pi-hole Prometheus Exporter
- Prometheus to scrape pihole-exporter
- Grafana to visualize Prometheus data

### deployment

1. Update `pihole-api-token.txt` with the Pi-hole API token.
1. Run `docker compose up` to simplify visualizing logs.
1. Run `docker compose up -d` to run the containers long term in detached mode.
1. In Grafana add our Prometheus deployment as a data source.
1. In Grafana import dashboard JSON from [here](https://github.com/eko/pihole-exporter)
