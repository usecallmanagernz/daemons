# TVS Installation

The following commands are for Ubuntu, you may need to adjust some
them for a different distributions.

## Create User, Paths and Install Programs

```
sudo useradd tvs -d /var/lib/tvs -s /usr/sbin/nologin
sudo mkdir -p /var/lib/tvs
sudo chown tvs:tvs /var/lib/tvs
sudo cp tvsctl tvsd tvsc /usr/bin
```

## Add Certificates to Database Using tvsctl

See https://usecallmanager.nz/trust-verification.html#tvsctl 

## Enable systemd Service

```
sudo cp systemd.tvs.service /etc/systemd/system/tvs.service
sudo systemctl daemon-reload
sudo systemctl enable tvs
sudo systemctl start tvs
```

## Show Service Logs

To see the output from the service run the following command.

```
journalctl -u tvs
```
