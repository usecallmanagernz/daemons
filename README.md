[![Workflow Status](https://img.shields.io/github/workflow/status/usecallmanagernz/daemons/python%20lint/master?label=python%20lint)](https://github.com/usecallmanagernz/daemons/actions/workflows/pylint.yml) [![Workflow Status](https://img.shields.io/github/workflow/status/usecallmanagernz/daemons/shell%20lint/master?label=shell%20lint)](https://github.com/usecallmanagernz/daemons/actions/workflows/shellcheck.yml) [![Version](https://img.shields.io/github/v/tag/usecallmanagernz/daemons?color=blue&label=version&sort=semver)](https://github.com/usecallmanagernz/daemons/releases) [![Licence](https://img.shields.io/github/license/usecallmanagernz/daemons?color=red)](LICENSE)

# Security Daemons 

Services and clients that do security services for phones

* `tvsd` - Server that responds to TVS requests. 
* `tvsctl` - Mange the certificate database used by `tvsd`.
* `tvsc` - Client that can send TVS requests. 
* `capfd` - Server that responds to CAPF requests.
* `capfctl` - Manage the device database used by `capfd`
* `capfc` - Client that can send CAPF requests.

See [Trust Verification](http://usecallmanager.nz/trust-verification.html) and
See [Certificate Enrollment](http://usecallmanager.nz/certificate-enrollment.html)
for example usage.

## Requirements

The following non-standard Python modules are required: `crytography`.

You can use the packages provided by your OS distribution or run
`sudo pip3 install -r requirements.txt` to satisfy those dependancies.

## TVS Installation

The following commands are for Ubuntu, you may need to adjust some
them for a different distributions.

### Create User, Paths and Install Programs

```
sudo useradd tvs -d /var/lib/tvs -s /usr/sbin/nologin
sudo mkdir -p /var/lib/tvs
sudo chown tvs:tvs /var/lib/tvs
sudo cp tvsctl tvsc /usr/local/bin
sudo cp tvsd /usr/local/sbin
```

Optionally, install the bash tab-completion helpers.

```
sudo cp bash_completion \
    /etc/bash_completion.d/usecallmanagernz-daemons
```

### Add Certificates to Database sing tvsctl

See https://usecallmanager.nz/trust-verification.html#tvsctl

```
sudo -u tvs /usr/local/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/ssl/private/sast.pem -s

sudo -u tvs /usr/local/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/asterisk/keys/asterisk.pem -c

sudo -u tvs /usr/local/bin/tvsctl /var/lib/tvs/tvs.sqlite3 \
    -i /etc/apache2/ssl-certs/apache.pem -a

...
```

### Enable systemd Service

```
sudo cp systemd.tvs.service /etc/systemd/system/tvs.service
sudo systemctl daemon-reload
sudo systemctl enable tvs
sudo systemctl start tvs
```

### Show Service Logs

To see the output from the service run the following command.

```
journalctl -u tvs
```

## CAPF Installation

The following commands are for Ubuntu, you may need to adjust some
them for a different distributions.

### Create User, Paths and Install Programs

```
sudo useradd capf -d /var/lib/capf -s /usr/sbin/nologin
sudo mkdir -p /var/lib/capf
sudo chown capf:capf /var/lib/capf
sudo cp capfctl capfc /usr/local/bin
sudo cp capfd /usr/local/sbin
```

Optionally, install the bash tab-completion helpers.

```
sudo cp bash_completion \
    /etc/bash_completion.d/usecallmanagernz-daemons
```

### Add Devices to Database Using capfctl

See https://usecallmanager.nz/certificate-enrollment.html#capfctl

```
sudo -u capf /usr/local/bin/capfctl /var/lib/capf/capf.sqlite3 \
  -s SEP58971ECC97C1 -o INSTALL

sudo -u capf /usr/local/bin/capfctl /var/lib/capf/capf.sqlite3 \
  -s SEP58971ECD8532 -o INSTALL

...
```

### Enable systemd Service

```
sudo cp systemd.capf.service /etc/systemd/system/capf.service
sudo systemctl daemon-reload
sudo systemctl enable capf
sudo systemctl start capf
```

### Show Service Logs

To see the output from the service run the following command.

```
journalctl -u capf
```
