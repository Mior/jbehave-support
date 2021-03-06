[Contents](../README.md)

## Reporting
There is an out of the box support prepared for XML reports to be generated for each story as well as creating an index file with links to each report.

To use this feature all that is needed is to register a bean of type XmlReporterFactory, e.g.:
```
@Bean
public XmlReporterFactory xmlReporterFactory() {
    return new XmlReporterFactory();
}
```

The generated XML report by default contains only information about:
 - story start time
 - story end time
 - story duration
 - story status (e.g. failed, successful)
 - story steps


### Reporter extensions
The default report can be extended with other info by registering beans implementing the interface XmlReporterExtension 
(for convenience an abstract class AbstractXmlReporterExtension containing methods for writing XML elements can be used).

There are several extensions already prepared and ready to use:
 - `EnvironmentInfoXmlReporterExtension` (copies Spring Environment properties starting with name `environmentInfo`)
 - `RestXmlReporterExtension` (copies REST requests/responses from [RestServiceSteps](Rest-api.md))
 - `WsXmlReporterExtension` (copies SOAP requests/responses from [WebServiceSteps](Web-service.md))
 - `TestContextXmlReporterExtension` (copies contents of [TestContext](Test-context.md))
 - `ServerLogXmlReporterExtension` (copies server log(s) for each system with configured [SshTemplate](Ssh.md))
- `FailScreenshotsReporterExtension` (prints out error screenshots from [Web testing](Web-testing.md) - if any were generated)

To use these extensions simply register the wanted extension as a bean, e.g.:
```
@Bean
public WsXmlReporterExtension wsXmlReporterExtension() {
    return new WsXmlReporterExtension();
}
```

---
