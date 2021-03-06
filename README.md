# TM4J Cucumber Integration Calculator Example

This is an example project on how to use the integration of
[Test Management for Jira](https://marketplace.atlassian.com/apps/1213259/tm4j-test-management-for-jira)
and automated tests when using Cucumber.

The integration is based on the JSON output files generated by Cucumber, so this output option needs to be
configured properly.

For more information about this example, please check out this [blog post](https://www.adaptavist.com/blog/an-essential-guide-to-agile-testing-with-bdd-inside-jira/)

For detailed information about how to integrate TM4J with Jenkins using BDD, please check out the documentation
for [TM4J Server](https://www.adaptavist.com/doco/display/KT/Test+Management+for+Jira+Server)
or [TM4J Cloud](https://www.adaptavist.com/doco/display/TMFJC/Test+Management+for+JIRA+Cloud)

Should you need any support from the Adaptavist team for configuring or using TM4J, please get in touch with us
through [our support portal](https://productsupport.adaptavist.com/servicedesk/customer/portals).

## Usage

Firstly, the JSON output format for Cucumber needs to be configured on the TestRunner class:
```
@RunWith(Cucumber.class)
@CucumberOptions(
        features = "src/test/resources/calculatorFeatures"
        ,glue={"com/adaptavist/tm4j/examples/cucumber/calculator"}
        ,plugin = {"json:target/cucumber/calculator.json"}
)
public class TestRunner {

}
```

The next step is to have a BDD test case in TM4J with the following test scenario:
```
Given a calculator I just turned on
When I input the number <a>
And I input the number <b>
And I press the multiplication button
Then I should see the result <c> on the calculator display

Examples:
| a  | b  | c   |
| 12 | 5  | 60  |
| 20 | 5  | 100 |
```

Now, you can use the REST API of TM4J ([Cloud API](https://docs.adaptavist.io/tm4j/cloud/api/v2/)
or [Server API](https://docs.adaptavist.io/tm4j/server/api/v1/)),
or use the [TM4J Jenkins plugin](https://plugins.jenkins.io/tm4j-automation) to download features files from TM4J.
Once the feature files are downloaded to the same directory configured on the `TestRunner`, they can be executed.
Optionally, the test results can be pushed back to TM4J.
