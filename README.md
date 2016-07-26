# h2specd
A testing tool for HTTP2 browser implementation.

### BINARY FILE:

Can be found in the [Releases section](https://github.com/Certerazvi/h2specd/releases), with the name "h2specd” and followed by the OS and architecture it is destined for. Download the one suitable for you.

### INSTRUCTIONS:

**a)** In order to create an https server on your localhost you need a self-signed certificate, which can be generated. You are recommended to run this command in the folder of the binary file so you do not have to move files around.

    % openssl req -x509 -newkey rsa:2048 -keyout localhost.key -out localhost.crt -days <DAYS> -nodes

**b)** Currently there are no options available hence the binary file should be run as it this, through the terminal. Make sure to run the file with root permissions (this is the case because in order to listen to a port destined for https, root rights are needed). For Linux and MacOS, type:

    % sudo ./h2specd

**c)** Once the program is running you can access the localhost through your browser and enter “https://localhost:443/XXX” as the address, where XXX represents the section number (based from the RFC 7540 specification) that you want to check in your browser.

**d)** After following the above mentioned guidelines a short description will appear about the test chosen followed by a PASSED or FAILED notification. Again, this will only appear in your terminal.

\*\* At the moment it is necessary to **force close** and **restart** the binary file in order to test other cases.

### ISSUES:

The source code is based on the net/http golang library, which was modified in certain places (namely server.go and h2_bundle.go) to be able to create tests that focus on extreme cases. Feedback is welcomed on the style, structure and implementation of h2specd. This still represents a work in progress.

Known issues are that the test cases:

* testCaseIllegalFrameSentWhileIdle
* testCaseSelfDependingPriorityFrame
* testCaseIllegalSizeRST_STREAM
* testCaseNonZeroLengthAckSettingFrame

do not seem to function as they should when checking them through Wireshark. No GOAWAY frame or a different error than the one expected and specified in RFC 7540 is received. These are results from trying the latest version of the Chrome browser.
