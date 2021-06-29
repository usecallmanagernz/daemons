[![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/usecallmanagernz/daemons/python%20lint/master?label=python%20lint)](https://github.com/usecallmanagernz/daemons/actions/workflows/pylint.yml) [![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/usecallmanagernz/daemons?color=blue&label=version&sort=semver)](https://github.com/usecallmanagernz/daemons/releases)

# Security Daemons 

Services and clients that do security services for phones

* `tvsd` - Server that responds to TVS requests. 
* `tvsctl` - Mange the certificate database used by `tvsd`.
* `tvsc` - Client that can send TVS requests. 

See [Trust Verification](http://usecallmanager.nz/trust-verification.html) for
example usage.

## Requirements

The following non-standard Python modules are required: `crytography`.

You can use the packages provided by your OS distribution or run
`sudo pip3 install -r requirements.txt` to satisfy those dependancies.
