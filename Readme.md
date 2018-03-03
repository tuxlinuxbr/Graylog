# List of Content pack

This repo have a list of content packs created from my client needs.

## Ufdb-Block Content Pack

This content pack possible you to add Ufdb logs in to Graylog to analise statistics from blocked websites.

### Getting Started

Import the ContentPack/ufdb_block_content-pack.json on your Graylog.

For configuration, you need add this values on /etc/rsyslog.d/ufdb-block.conf file, changing **GRAYLOG_NAME_SERVER** for the hostname or ip address of the Graylog server.

```
# Load Modules
module(load="imfile")
module(load="omfwd")
input(type="imfile"
         File="/var/log/ufdbguard/ufdbguardd.log"
         Tag="ufdb-block"
         Severity="info"
         Facility="local7"
         ruleset="UfdbForward")

ruleset(name="UfdbForward") {
        if $msg contains 'BLOCK' then
                action(type="omfwd"
                Target="GRAYLOG_NAME_SERVER"
                Port="19202"
                Protocol="tcp"
                template="RSYSLOG_SyslogProtocol23Format")
}
```
### Prerequisites

Graylog and Syslog-TCP input.

## Authors

* **Renan Schiavo** - *Initial work* - (https://github.com/tuxlinuxbr/Graylog)

## License

This project is licensed under the Apache License - see the [LICENSE.md](LICENSE.md) file for details
