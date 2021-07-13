# TVS Installation

The following commands are for Ubuntu, you may need to adjust some
them for a different distributions.

## Create User, Paths and Install Programs

```
sudo useradd tvs -d /var/lib/tvs -s /usr/sbin/nologin
sudo mkdir -p /var/lib/tvs
sudo chown tvs:tvs /var/lib/tvs
sudo cp tvsctl tvsc /usr/bin
sudo cp tvsd /usr/sbin
```

## Add Certificates to Database Using tvsctl

See https://usecallmanager.nz/trust-verification.html#tvsctl 

```
sudo -u tvs /usr/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/ssl/private/sast.pem -s

sudo -u tvs /usr/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/asterisk/keys/asterisk.pem -c

sudo -u tvs /usr/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/apache2/ssl-certs/apache.pem -a

...
```

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

# CAPF Installation

The following commands are for Ubuntu, you may need to adjust some
them for a different distributions.

## Create User, Paths and Install Programs

```
sudo useradd capf -d /var/lib/capf -s /usr/sbin/nologin
sudo mkdir -p /var/lib/capf
sudo chown capf:capf /var/lib/capf
sudo cp capfctl capfc /usr/bin
sudo cp capfd /usr/sbin
```

## Add Devices to Database Using capfctl

See https://usecallmanager.nz/certificate-enrollment.html#capfctl

```
sudo -u capf /usr/bin/capfctl /var/lib/capf/capf.sqlite3 \
  -s SEP58971ECC97C1 -o INSTALL

sudo -u capf /usr/bin/capfctl /var/lib/capf/capf.sqlite3 \
  -s SEP58971ECD8532 -o INSTALL

...
```

## Enable systemd Service

```
sudo cp systemd.capf.service /etc/systemd/system/capf.service
sudo systemctl daemon-reload
sudo systemctl enable capf
sudo systemctl start capf
```

## Show Service Logs

To see the output from the service run the following command.

```
journalctl -u capf
```
