
Create a architcture based following the principles of reutilizable systems.

/*Explicit the architcture, like framework we will use*/
1. Framework/
    /core ->
    /api ->
    /mobile ->
    /web -> all web tests
    /web/helpers/resources

2. API Testing (Kotlin + RestAssured / Ktor / OkHttp) 

How you would model requests/responses 
we can create files that we can use in the different tests (like we can call all this files using the same and reusable)
* note: Here e can set all request json, response json, and use it to create a method that we just set all this files.

How you would reuse a shared API client 
Note: Like a login off our application, it's a good way to reuse this method that we call and just pass the token of our aplication.

exp:

def login ()
{
    request.url(localhost/login)
    token_application = response.body('berer token')
}

beforeAll (){
    login.new
}

How you would handle environments (e.g., env.yaml file) 
2.1. We can set use a application yml to set all environment that we have, and just set this infomation while we call (npm run dev, or npm run prd)

exp: 

ENV_DEV_URL - localhost/dev
ENV_PRD_URL - localhost/prod

gradle.build

test {
    system.Properties System.properties
}

./gradlew sessionTest -Denv=dev
./gradlew sessionTest -Denv=prd


3. Web UI Automation (Selenium or Cypress)

3.1 - Use of the Page Object Model 

This is a good practice to set a POM design pattern because we can reuse and made our test more clean.
Just create a folders we can call: elements/method/implementation

Elements: We will create a library with all elements that we have.
exp: LOGIN_VAR = xpath('someXpath') or EMAIL_VAR = selenium.webdriver.id('SOMEID')

Method folder: We will call all this elements and create methods to use that.

def LOGIN () {
    seleniumWebDriver.elements.id(login_var)
}

Implementation Folder:

import method_file
it ('Login in our application) -> {
    LOGIN
}

3.2 - Handling of waits 

Until - We can use until (function) that our application will wait the response of some method or some elements or payload of or website 

Sleep - We can set also sleep thread in our application just wait a moment to payload our application also. But in this case if we set a time like 10 sec and our application spend 11 sec, our test will crash and fail.

WebDriverWait - We can use also webDriverWait together with until.

3.3 - Local vs. remote execution (Selenium Grid) 

If we run some test use local environment we need to garanfy if our application is available to run it. We just set using testSession to run localy some test using tag (@test, @testRegressive, @login)

If we use a pipeline to run our test, just start the step of test on the pipeline.
not: Is a good pratice to create to separete test pipeline to start it only. unless to start all entire application.

We can create a 2 pipeline (1 - Application, 1 - Tests), and integrate it after.

Exp:

step1 - Build Application - Step 2 - Run unit test - Step 3 Run Automation Test (call another pipeline o just set here the code to run it). Get report for pipeline test

pipeline test

step1 - Build tests application - Step2 - Run tests - Step 3 - Send report for another pipeline
