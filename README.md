avs-device-sdk-intel-speech-enabling-kit
Significant changes have been made to the authorization process and the `AlexaClientSDKConfig.json` configuration file in v1.7 of the AVS Device SDK. [Click here for update instructions](https://github.com/alexa/avs-device-sdk/wiki/Code-Based-Linking----Configuration-Update-Guide).
If you are updating from v1.3 or earlier to v1.6, you must update your `AlexaClientSDKConfig.json` to include a Notifications database. An updated sample is available in the quickstart guides for Ubuntu Linux, Raspberry Pi, macOS, and Generic Linux.

See [release notes](https://github.com/alexa/avs-device-sdk#release-notes-and-known-issues) for a complete list of updates, enhancements, bug fixes, and known issues for this release.
### Security Best Practices

In addition to adopting the `Security Best Practices for Alexa`[https://developer.amazon.com/docs/alexa-voice-service/security-best-practices.html], when building the SDK:

* Protect configuration parameters, such as those found in the AlexaClientSDKCOnfig.json file, from tampering and inspection.
* Protect executable files and processes from tampering and inspection.
* Protect storage of the SDK's persistent states from tampering and inspection.
* Your C++ implementation of AVS Device SDK interfaces must not retain locks, crash, hang, or throw exceptions.
* Use exploit mitigation flags and memory randomization techniques when you compile your source code, in order to prevent vulnerabilities from exploiting buffer overflows and memory corruptions.

v1.7.0 released 04/17/2018:
* `AuthDelegate` and `AuthServer.py` have been replaced by `CBLAUthDelegate`, which provides a more straightforward path to authorization.
* Added a new configuration property called [`cblAuthDelegate`](https://github.com/alexa/avs-device-sdk/blob/master/Integration/AlexaClientSDKConfig.json#L2). This object specifies parameters for `CBLAuthDelegate`.
* Added a new configuration property called [`miscDatabase`](https://github.com/alexa/avs-device-sdk/blob/master/Integration/AlexaClientSDKConfig.json#L34), which is a generic key/value database to be used by various components.
* Added a new configuration property called [`dcfDelegate`](https://github.com/alexa/avs-device-sdk/blob/master/Integration/AlexaClientSDKConfig.json#L17) This object specifies parameters for `DCFDelegate`. Within this object, values were added for the 'endpoint' and `overridenDcfPublishMessageBody`. 'endpoint' is the endpoint to connect to in order to send device capabilities. `overridenDcfPublishMessageBody`is the message that will get sent out to the Capabilities API. Note: values within the `dcfDelegate` object will only work in `DEBUG` builds.
* Added a new configuration property called [`deviceInfo`](https://github.com/alexa/avs-device-sdk/blob/master/Integration/AlexaClientSDKConfig.json#L9) which specifies device-identifying information for use by the Device Capability Framework (DCF), and for authorization (CBLAuthDelegate).
* Updated the Directive Sequencer to support wildcard directive handlers. This allows a handler for a given AVS interface to register at the namespace level, rather than specifying the names of all directives within that namespace.
* Updated the Raspberry Pi installation script to include `alsasink` in the configuration file.
* Added `audioSink` as a configuration option. This allows users to override the audio sink element used in `Gstreamer`.
* Added an interface for monitoring internet connection status: `InternetConnectionMonitorInterface.h`.
* The Alexa Communications Library (ACL) is no longer required to wait until authorization has succeeded before attempting to connect to AVS. Instead, `HTTP2Transport` handles waiting for authorization to complete.
* Added the Device Capabilities Framework (DCF) delegate. Device capabilities can now be sent for each capability interface using DCF publish messages.
* The sample app has been updated to send DCF publish messages, which will automatically occur when the sample app starts. Note: a DCF publish message must be successfully sent in order for communication with AVS to occur.
* The SDK now supports HTTP PUT messages.
* Added support for opt-arg style arguments and multiple configuration files. Now, the sample app can be invoked by either of these commands: `SampleApp <configfile> <debuglevel>` OR `SampleApp -C file1 -C file2 ... -L loglevel`.
* [Issue 400](https://github.com/alexa/avs-device-sdk/issues/400) Fixed a bug where the alert reminder did not iterate as intended after loss of network connection.
* [Issue 477](https://github.com/alexa/avs-device-sdk/issues/477) Fixed a bug in which Alexa's weather response was being truncated.
* Fixed an issue in which there were reports of instability related to the Sensory engine. To correct this, the `portAudio` [`suggestedLatency`](https://github.com/alexa/avs-device-sdk/blob/master/Integration/AlexaClientSDKConfig.json#L62) value can now be configured.
* Fixed a bug in which alerts failed to activate if the system was restarted without network connection.
* Fixed Android 64-bit build failure issue.
* Some ERROR messages may be printed during start-up event if initialization proceeds normally and successfully.
* If an unrecoverable authorization error or an unrecoverable DCF error is encountered, the sample app may crash on shutdown.
* If a non-CBL `clientId` is included in the `deviceInfo` section of `AlexaClientSDKConfig.json`, the error will be reported as an unrecoverable authorization error, rather than a more specific error.
