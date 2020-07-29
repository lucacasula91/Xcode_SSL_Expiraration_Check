# Xcode_SSL_Expiraration_Check
This script simply check the total of the remaining seconds to the certificate expiration.
In case the threshold is less than **45 days** Xcode raise an error and the build fails just to remind the developer to renew the ssl certificate.


## Xcode implementation
![SSL_Checker_Xcode_1](http://lucacasula.it/GitHubImages/SSL_Checker_Xcode_1.png)

![SSL_Checker_Xcode_2](http://lucacasula.it/GitHubImages/SSL_Checker_Xcode_2.png)

```bash
echo "CHECKS THE EXPIRATION DATE FOR SSL CERTIFICATE"

INPUTFILE=$SCRIPT_INPUT_FILE_0
let SECONDSIN24HOURS=86400
let THRESHOLDDAYS=45
let THRESHOLDEXPIRATION=$SECONDSIN24HOURS*$THRESHOLDDAYS

echo $THRESHOLDEXPIRATION

if openssl x509 -checkend $THRESHOLDEXPIRATION -noout -in "$INPUTFILE"
then
echo "warning: Certificate is good for at least 45 days!"
exit 0

else
echo "error: Certificate has expired or will do so within 24 hours!"
exit 1

fi
```

![SSL_Checker_Xcode_3](http://lucacasula.it/GitHubImages/SSL_Checker_Xcode_3.png)
