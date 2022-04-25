# RStudio Nagios Plugins

## Check RStudio products

Runs simple product availability checks on all products.

``` bash
./check_rstudio --help
```

    usage: check_rstudio [-h] [-H HOSTNAME] [-w WARNING] [-c CRITICAL]
                         [-p PRODUCT] [-P PATH] [-n NUMBER] [-D] [-i] [-t TIMEOUT]
                         [-d]

    optional arguments:
      -h, --help            show this help message and exit
      -H HOSTNAME, --hostname HOSTNAME
                            Hostname of the system to check
      -w WARNING, --warning WARNING
                            Warning threshold
      -c CRITICAL, --critical CRITICAL
                            Critical threshold
      -p PRODUCT, --product PRODUCT
                            RStudio product
      -P PATH, --path PATH  set a url path
      -n NUMBER, --number NUMBER
                            Number of repeats
      -D, --dryrun          Don't perform the check
      -i, --insecure        use http instead of https
      -t TIMEOUT, --timeout TIMEOUT
                            timeout in seconds
      -d, --debug           enable debug mode

For example:

``` default
$ check_rstudio -H rstudio.example.com --product connect -P rsc
OK - Status endpoint is reachable
```

possible values for `--product` (`-p`) include:

-   connect
-   workbench
-   packagemanager

## Check RStudio Workbench

Performas a detailed check of RStudio Workbench installations.

eg:

``` default
$ check_workbench -H colorado.rstudio.com -P rstudio -o license-days-left -w 30 -c 10
CRITICAL: license-days-left is 3
```

Check the memory percentage:

``` default
$ check_workbench -H colorado.rstudio.com -P rstudio -o memory-percent -w 60 -c 80
WARNING: memory-percent is 66.3
```

Possible values for `--option` (`-o`) are:

-   active-sessions
-   idle-seconds
-   cpu-percent
-   memory-percent
-   swap-percent
-   load-average
-   license-days-left
-   license-allow-product-usage

Full help output:

``` bash
./check_workbench --help
```

    usage: check_workbench [-h] [-H HOSTNAME] [-w WARNING] [-c CRITICAL]
                           [-o OPTION] [-P PATH] [-D] [-i] [-t TIMEOUT] [-d]

    optional arguments:
      -h, --help            show this help message and exit
      -H HOSTNAME, --hostname HOSTNAME
                            Hostname of the system to check
      -w WARNING, --warning WARNING
                            Warning threshold
      -c CRITICAL, --critical CRITICAL
                            Critical threshold
      -o OPTION, --option OPTION
                            item to check
      -P PATH, --path PATH  set a url path
      -D, --dryrun          Don't perform the check
      -i, --insecure        use http instead of https
      -t TIMEOUT, --timeout TIMEOUT
                            timeout in seconds
      -d, --debug           enable debug mode

### RStudio Workbench health-check example

RStudio Workbench docs on the [health-check
endpoint](https://docs.rstudio.com/ide/server-pro/auditing_and_monitoring/server_health_checks.html)

Example output:

``` default
active-sessions: 1
idle-seconds: 0
cpu-percent: 0.0
memory-percent: 64.2
swap-percent: 0.0
load-average: 4.1
license-status: Activated
license-days-left: 153
license-allow-product-usage: 1
```

## Notes

### Nagios exit codes

-   OK - exit 0
    -   output example - “OK: message goes here”
-   WARNING - exit 1
    -   output example - “WARNING: message goes here”
-   CRITICAL - exit 2
    -   output example - “CRITICAL: message goes here”
-   UNKNOWN - exit 3
    -   output example - “UNKNOWN: message goes here”
