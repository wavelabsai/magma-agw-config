# Access Gateway Configuration

First, copy the root CA for your Orchestrator deployment into your AGW:
```bash
scp rootCA.pem root@172.16.4.72:/var/opt/magma/tmp/certs/rootCA.pem
```
---

Point AGW to the following contents into the file:
```bash
vim /var/opt/magma/configs/control_proxy.yml
```

Put the following contents into the file:
```yaml
cloud_address: controller.magmasi.wavelabs.in
cloud_port: 443
bootstrap_address: bootstrapper-controller.magmasi.wavelabs.in
bootstrap_port: 443
fluentd_address: fluentd.magmasi.wavelabs.in
fluentd_port: 24224

rootca_cert: /var/opt/magma/tmp/certs/rootCA.pem
```
---

Then restart your services to pick up the config changes:
```bash
sudo service magma@* stop
sudo service magma@magmad restart
```

Ref: https://docs.magmacore.org/docs/lte/deploy_config_agw
