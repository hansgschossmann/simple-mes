# simple-mes

simple-mes is an OPC UA client and implements a simple Manufacturing Exection System to control a production line build of stations which are available as docker containers as well.
The MES controls three stations (Assembly, Test, Packaging) of the production line. To connect to these stations, the OPC UA endpoint URLs must be passed in via command line parameters.
If they are ommited, then the MES expects the stations on different ports on the same host as the MES is running (Assembly: 51210, Test: 51211, Packaging: 51212).

The implementation of the station can be found [here](https://github.com/hansgschossmann/simple-station). The container is available [here](https://hub.docker.com/r/hansgschossmann/simple-station).

A docker container of this repository is available [here](https://hub.docker.com/r/hansgschossmann/simple-mes).


The MES supports shift configuration via the command line options `--fs`, `--sl`, `--ss`, `--sc`, and `--dw`. As soon as one of those options is specified, the shift control is enabled.
If none of these options is specified, then shift control is not used.

Purpose of the shift control is to allow deploying production lines in different time zones using the container timezone setting. To enable this in the containerized version you need to set the timezone of the container.



# Usage

    Current directory is: C:\Repos\hg\simple-mes\bin\Debug\netcoreapp3.1
    Log file is:
    Log level is: info
    SimpleMes V1.0.0.0 (Informational Version: 1.0.0+0025abdec7)
    Usage: SimpleMes.exe [<options>]
   
    Options:
          --as, --assemblystation=VALUE
                                 the endpoint of the assemblystation
                                   Default: 'opc.tcp://johannglt:51210'
          --ts, --teststation=VALUE
                                 the endpoint of the teststation
                                   Default: 'opc.tcp://johannglt:51211'
          --ps, --packagingstation=VALUE
                                 the endpoint of the packagingstation
                                   Default: 'opc.tcp://johannglt:51212'
          --fs, --firstshiftstart=VALUE
                                 time the work starts every day (24hr format: hhmm)
                                   Default: '0600'
          --sl, --shiftlength=VALUE
                                 shift length in minutes
                                   Min: 5
                                   Max: 1440
                                   Default: '480'
          --ss, --shiftshouldstart=VALUE
                                 percent when we still should start a shift
                                   Min: 0
                                   Max: 1
                                   Default: '0,9'
          --sc, --shiftcount=VALUE
                                 number of shifts per day
                                   Default: '3'
          --dw, --daysperweek=VALUE
                                 number of working days per week starting monday
                                   Default: '0'
          --lf, --logfile=VALUE  the filename of the logfile to use.
                                   Default: 'johannglt-mes.log'
          --ll, --loglevel=VALUE the loglevel to use (allowed: fatal, error, warn,
                                   info, debug, verbose).
                                   Default: info
          --aa, --autoaccept     auto accept station server certificates
                                   Default: 'False'
          --to, --trustowncert   the applications certificate is put into the
                                   trusted certificate store automatically.
                                   Default: False
          --at, --appcertstoretype=VALUE
                                 the own application cert store type.
                                   (allowed values: Directory, X509Store)
                                   Default: 'Directory'
          --ap, --appcertstorepath=VALUE
                                 the path where the own application cert should be
                                   stored
                                   Default (depends on store type):
                                   X509Store: 'CurrentUser\UA_MachineDefault'
                                   Directory: 'pki/own'
          --tp, --trustedcertstorepath=VALUE
                                 the path of the trusted cert store
                                   Default 'pki/trusted'
          --rp, --rejectedcertstorepath=VALUE
                                 the path of the rejected cert store
                                   Default 'pki/rejected'
          --ip, --issuercertstorepath=VALUE
                                 the path of the trusted issuer cert store
                                   Default 'pki/issuer'
          --csr                  show data to create a certificate signing request
                                   Default 'False'
          --ab, --applicationcertbase64=VALUE
                                 update/set this applications certificate with the
                                   certificate passed in as bas64 string
          --af, --applicationcertfile=VALUE
                                 update/set this applications certificate with the
                                   certificate file specified
          --pb, --privatekeybase64=VALUE
                                 initial provisioning of the application
                                   certificate (with a PEM or PFX fomat) requires a
                                   private key passed in as base64 string
          --pk, --privatekeyfile=VALUE
                                 initial provisioning of the application
                                   certificate (with a PEM or PFX fomat) requires a
                                   private key passed in as file
          --cp, --certpassword=VALUE
                                 the optional password for the PEM or PFX or the
                                   installed application certificate
          --tb, --addtrustedcertbase64=VALUE
                                 adds the certificate to the applications trusted
                                   cert store passed in as base64 string (multiple
                                   strings supported)
          --tf, --addtrustedcertfile=VALUE
                                 adds the certificate file(s) to the applications
                                   trusted cert store passed in as base64 string (
                                   multiple filenames supported)
          --ib, --addissuercertbase64=VALUE
                                 adds the specified issuer certificate to the
                                   applications trusted issuer cert store passed in
                                   as base64 string (multiple strings supported)
          --if, --addissuercertfile=VALUE
                                 adds the specified issuer certificate file(s) to
                                   the applications trusted issuer cert store (
                                   multiple filenames supported)
          --rb, --updatecrlbase64=VALUE
                                 update the CRL passed in as base64 string to the
                                   corresponding cert store (trusted or trusted
                                   issuer)
          --uc, --updatecrlfile=VALUE
                                 update the CRL passed in as file to the
                                   corresponding cert store (trusted or trusted
                                   issuer)
          --rc, --removecert=VALUE
                                 remove cert(s) with the given thumbprint(s) (
                                   multiple thumbprints supported)
      -h, --help                 show this message and exit

