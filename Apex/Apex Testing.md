# Apex Testing

## General

Apex tests are critical for quality assurance and are required for deploying and distributing Apex from a sandbox to a production org

Before each service upgrade, Salesforce automatically runs all Apex tests in your org for you via a process called Apex Hammer

- Runs both in current version & in next release's version & compares test results

### Test Class Syntax

    @isTest public class `test_class_name` {
        ... `code to execute` ...
    }

### Test method syntax

    @isTest static void `test method name()` {
        ... `code to execute`
    }

- _Visibility of a test method doesn't matter_
  - declaring a test method public/private doesn't make a difference
  - For this reason, just omit access modifiers in the definition syntax

- Sometimes an issue with the Developer Console prevents it from updating code coverage percentages correctly when running only a subset of tests
  - To update code coverage results correctly, opt to run all tests rather than simply a new test run
- A __test suite__ is a collection of Apex test classes that are run together
  - Can create in Developer Console to define set of classes to execute together regularly
- Salesforce records created in test methods are not committed to database; rolled back when test execution finishes
- By default, Apex tests do no have access to pre-existing org data (except setup & metadata objects; user, profile, etc.)
  - If for some reason your test method needs to access pre-existing data in the Salesforce database, annotate the test method with `@isTest(SeeAllData = true)`
- Test methods cannot:
  - Send emails
  - Make callouts to external services; use mock callouts in tests
  - Return SOSL search results; SOSL searches in test always return empty results
    - Use `Test.setFixedSearchResults()` to define records expected to be returned by the search
- `Test.startTest()` and `Test.stopTest()` can be used in the middle of a test method's body to specify exactly where the code to be tested is
  - E.g. if some code exists in the body to instantiate a record to test with other code later on, can use these delimiters to only test the code later on
  - Code inside the delimiters is allocated a fresh set of governor limits
  - Used to __test future methods__
- If you need a lot of test data for a test class, good practice is to make a new class to host all the data and store it in methods accordingly
  - Referred to as a utility class
- A class such as a __TestDataFactory__ is a special kind of class if it is annotated with `@isTest`
  - Not the method(s), the __entire class__!
  - Can be accessed only from running a test
- Test utility classes are  excluded from org's code size limit

#### Example of a "mocked" callout to an external service for testing purposes

Mock callout class:

    @isTest
    global class SMSCalloutMock implements HttpCalloutMock {
        global HttpResponse respond(HttpRequest req) {
            // Create a fake response
            HttpResponse res = new HttpResponse();
            res.setHeader('Content-Type', 'application/json');
            res.setBody('{"status":"success"}');
            res.setStatusCode(200);
            return res;
        }
    }

Mock test class:

    @IsTest
    private class Test_SMSUtils {
        @IsTest
        private static void testSendSms() {
            Test.setMock(HttpCalloutMock.class, new SMSCalloutMock());
            Test.startTest();
            SMSUtils.sendSMSAsync('111', '222', 'Greetings!');
            Test.stopTest();
            // runs callout and check results
            List<SMS_Log__c> logs = [select msg__c from SMS_Log__c];
            System.assertEquals(1, logs.size());
            System.assertEquals('success', logs[0].msg__c);
        }
    }

- `Test.isRunningTest()` checks if Apex is running in a test context
  - Useful for testing queueable jobs; can't chain together queueable jobs together for testing like you can in class construction
- `Test.setMock()` method lets runtime know that mock callouts are used in a test method
- For testing Apex REST class methods that don’t take parameters or rely on information from REST request, create a test request
  - Simulate a REST request by creating a RestRequest object in the test method, set properties accordingly

Example

    RestRequest request = new RestRequest();
    request.requestUri = 'https://yourInstance.salesforce.com/services/apexrest/Cases/' + recordId;
    request.httpMethod = 'GET';
    request.params.put('status', 'Working');
        ... other code to execute ...
    RestContext.request = request;

- Example above could vary with different objects in Salesforce; i.e. other fields could be updated in a .params.put() method other than 'status' with a value of 'Working'
