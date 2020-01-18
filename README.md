# Docker: One `nginx` ingress to `php:apache` containers

Add the following to Hosts file:

```bash
sudo tee --append /etc/hosts <<EOF

127.0.0.1   local.ac93.co.uk
127.0.0.1   local-crm.ac93.co.uk
127.0.0.1   local-api.ac93.co.uk
127.0.0.1   local-mem.ac93.co.uk
127.0.0.1   local-vip-mem.ac93.co.uk

EOF
```

| Host | XDebug Port |
|------|-------------|
| local.ac93.co.uk | 9103 |
| * | 9103 |
| local-crm.ac93.co.uk | 9100 |
| local-api.ac93.co.uk | 9101 |
| local-mem.ac93.co.uk | 9102 |
| local-vip-mem..ac93.co.uk | 9102 |
