# synack_burp

TLDR
If you don't want to be bothered use my cacerts file which is attached here and copy it on the location of yours.

For all java application the certificate trust is handled under 'cacerts' file.  As Burp is a java application you should locate the path
of this file.  You can identify the location of the file easier by looking on the Burp's directory structure or as Burp is running 

e.g.
```
[root@a-3ludabc security]# ps auxw | grep burp | grep java
PROD-LP+   371  0.4  4.4 8408768 719120 ?      Sl   Aug10  56:22 /home/srt_izabc/BurpSuitePro/jre/bin/java -splash:/home/srt_izabc/BurpSuitePro/.install4j/s_3eifkq.png --add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/javax.crypto=ALL-UNNAMED --add-opens java.desktop/javax.swing=ALL-UNNAMED -Xmx4096m -classpath /home/srt_iz7abc/BurpSuitePro/.install4j/i4jruntime.jar:/home/srt_iz7abc/BurpSuitePro/.install4j/launcherccf7dac9.jar:/home/srt_iz7habc/BurpSuitePro/burpsuite_pro.jar install4j.burp.StartBurp
```

From the above one can see that the java used by Burp is under `/home/srt_izabc/BurpSuitePro/jre/bin/java` on my system. 

The cacerts file is located under the path of jre/lib/security/ .

To view the contents of the file you can open it using `keytool -list -v -keystore cacerts` , the password which is the default is `changeit` 

On the default cacerts file you will need to import the CA of synack as trusted so calls that are originating from Burp itself ( collaborator/extensions ) 
are working normally.

To get synack's cert go to your LP+, open firefox -> Certificate Manager -> SYNACK-LAUNCHPOINT-SP and export the certificate. 
Be sure to select DER format from the options and change the extension on the filename to SYNACK-LAUNCHPOINT-SP.der.

To import SYNACK-LAUNCHPOINT-SP.der on your cacert file you use the following command:
`keytool -import -alias burp -keystore cacerts -file SYNACK-LAUNCHPOINT-SP.der`
When prompted for password use `changeit`


