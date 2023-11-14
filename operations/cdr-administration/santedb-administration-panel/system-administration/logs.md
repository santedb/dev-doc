# Logs



SanteDB server logs can be accessed using the Logs menu in the System panel. Logs allow system administrators to access either dCDR or iCDR log files from the web user interface directly.

![](<../../../../.gitbook/assets/image (407).png>)

When an administrator opens a log, a quick preview of the log contents are shown, and an option to download the entirety of the system log is provided. You may also optionally download a log from the local machine or the server using the `Download` option.

![](<../../../../.gitbook/assets/image (659).png>)

## Log Format

SanteDB iCDR and dCDR use a common logging format which can be easily parsed with a few regular expressions. In general the format of the log is:

```
Source.Name.Class@THREAD <Information|Warning|Error> [TIME-STAMP]: Message
```

![](<../../../../.gitbook/assets/image (552).png>)
