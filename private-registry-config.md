```
mkdir  /etc/docker/certs.d/devocr.paas.com

scp devocr.paas.com:/certs/domain.crt   /etc/docker/certs.d/devocr.paas.com/

cat /etc/docker/certs.d/devocr.paas.com/domain.crt    >> /etc/pki/tls/certs/ca-bundle.crt

```