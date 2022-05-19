
**Installing the Angular CLI**
npm install -g @angular/cli
Refer Following link for more details
https://github.com/angular-university/angular-testing-course/tree/1-start#angular-testing-course

# Angular-Testing-Cypress
ANGULAR -TESTING
•	Cyprus---end to end testing tool
1.	Selenium is same as cyprus but Cyprus Is Advanced 

Jasmine is a behavior-driven development framework for testing JavaScript code. It does not depend on any other JavaScript frameworks. It does not require a DOM. And it has a clean, obvious syntax so that you can easily write tests.
angulartest with utility:
 the angular test is going to allow us to provide the dependencies to our services by using dependency injection insteadof calling constructor's explicitly.

Execute particular specs or debugging only 1:
	Use f before function or debugging test case.We can also focus(f) on only one test and skip all the others.---to focus on particular case
	Use x before function or debugging test case. To didn’t run that particular test case
Ex:1
  xit("should substract two numbers", () => {
    console.log("substract test");
    // const calculator = new CalculatorService(new LoggerService());
    const result = calculator.subtract(2, 2);
    expect(result).toBe(0, "unexpected error in substract");
    // expect(loggerSpy.log).toHaveBeenCalledTimes(1);
  });
2.

  fit("should substract two numbers", () => {
    console.log("substract test");
    // const calculator = new CalculatorService(new LoggerService());
    const result = calculator.subtract(2, 2);
    expect(result).toBe(0, "unexpected error in substract");
    // expect(loggerSpy.log).toHaveBeenCalledTimes(1);
  });

Flush:
const req = httpTestingController.expectOne("/api/course");
    expect(req.request.method).toEqual("GET");
    //The argument that we are going to pass here to these Flesche Cole is going to be the test data returned by our mock request.
    req.flush({});
to run backend:
npm run server 
stop runner -------clear

Notes—angular testing master course—sec-4-video NO.33
We can write our tests in the usual setup where we will do some data set up first.
Then we are going to execute the test functionality and atleast we are going to have our test assertions
at the bottom of the test, just like if we were testing synchronous functionality.
Now let's use the fake async test utility and apply it to our home component where we have run into
a problem before it has forced us to use here set timeout in order to make sure that our assertions
are being executed.
So if you remember here, we used the combination of said timeout with the Jasmyn, then callback.
So let's revisit this test using fake async before doing so.
Let's switch here to our test examples and let's make sure that we remove here the focus from these
tests with these all artists are going to get executed again.
Now, going back here to our test suite, let's see, why did we have to use your set timeout and then
Jesmyn callback in this particular test?
So in this particular test, we are testing here the home component and we are making sure that whenever
we click here on the advanced courses doverton that the advanced courses get displayed instead of the
beginner courses.
So the way that the test is written is we are first going to set up here some data.
We are going to prepare here a list of courses that contains both beginner courses and advanced courses.
And we are going to return this at least here in the goal to find all courses.
So here this test in the before each class is setting up here a component as usual, and it's also setting
up here Accorsi service using a mock version that will return our test data.
So going here to our test that is using set timeout, we are taking the mock the version of courses
service and we are passing here our list to the call final courses.
Next, we are applying here to the angular change detection functionality and we are updating the DOM
of our test with the list of courses.
So at this point in the test, we will expect to have a DOM containing the beginner courses and a button
here to enable the advanced courses.
So we are going to carry the DOM and we are going to return here at least of Tabart.
And so here we should get here an array with two Tabart and the Wegener's Button and the advanced Abberton.
Next, we are going to simulate here some user interaction.
We're going to click here on the second element of the array, which would correspond here to the advanced
courses tab button.
Then next we are going to call again angular change detection.
And it was at this point that we then realized that here at this specific point in the test, it was
not possible to confirm that the advanced courses were getting displayed.
So these assertions here, if they were to be added directly here at this point in the test immediately
after calling detect changes, the assertions would not return the expected results.
And this is because the component that we are testing uses here, this material type group component,
which has some asynchronous behavior built in.
So this component uses internally request animation frame in order to create here a smooth animation
in this transition between course lists.
So the use of these asynchronous broza prevents us from writing this test in a synchronous way.
So we ended up here calling set timeout, waiting for the animation to complete, and then here inside
the body of said timeout, we are then going to assert that indeed the advanced courses are now getting
displayed on the screen and after that we are then going to call the Jasmyn, then callback.
Otherwise the test is going to timeout and it's going to be considered as a field test.
Even though it's always possible to write our asynchronous test using the Jesmyn then callback, it
can become a bit confusing, this type of code.
I mean, ideally we would like take this assertion code that we are here inside our set timeout and
move it here right after the call to detect changes.
And ideally, we wouldn't have to use any sort of timeouts or callbacks in order to implement our tests.
So this will essentially be our ideal test to write.
This type of test looks like a normal test for synchronous functionality.
We are setting up here our test data.
We are executing the test and we are performing the test assertions in a sequential and readable way,
and most of all, we are not aware of the internal details of the component that we are testing.
We don't know in this type of code if the component calls request animation, frame set time timeout
or any other asynchronous EPA, we simply test the functionality, just like if it would be synchronous
functionality.
Well, using the angular fake async test zone, it's possible to write this test this way.
Let's see how first we are going to start by removing here the Jasmyn, then callback.
And as usual, we are going to apply here the fake async test utility that is going to wrap all the
code inside this test inside a fake async testing zone.
Now, this zone is going to keep track of all the asynchronous operations launched by the code here
inside our test block.
And this includes the call to request animation frame made by our course list component.
We will then, as we have seen before, need to use some fixing specific APIs in order to either move
time forward or Flesche the multiple event cues such as the microvascular or the fescue in order to
make the test pass.
So now that we have rewrapped here, our synchronous code in the Fakher Sync testing zone, let's have
a look at the current test results.
So as you can see here in the test report, we are still getting here that we cannot find the security
course after everything, click on the advanced courses tab.
But more importantly, we also have here a new error, saying that there is still one timer on the queue.
Now, we don't have any details about what is this type of timer, but we know that, by the way, that
the component is implemented, that this is a call to request animation frame.
Now, we don't have to know this information in order to test these asynchronous goal.
We know that some timer was triggered here by the component that we are testing.
And we know that before running our assertions, we want to make sure that the task Q is completely
empty before going forward.
So in order to ensure that we are going to adhere, as we have seen before, a call to flush.
So Flesche is going to empty the task.
You at this point in the test, let's now see what are the test results now.
So if we switch here to our report, we are going to see that our test is working correctly.
And also we can see that we don't have any errors in our console.
So the call to flesh is essentially empty the task.
Q So the task that was there that was called a timer in the error message has been processed and removed
from the queue.
So now the fake async test zone can consider this test as completed.
Notice that in order to fix this particular test, using Flesche micro tasks would not be sufficient.
Let's try this out just to confirm it.
If we now check the test results, we are going to see that we again get the error message.
There is still one timer on the queue.
So we know that the asynchronous operation that this component is launching is not a micro task.
It cannot be a promise.
For example, it has to be something else.
It has to be instead of a normal browser, tasks such as a set timeout, a set interval, or in this
particular case, a call to request animation frame.
So we really need to use Flesche here now because we know that this is a call to request animation frame.
We could also call here, take and pass it the value.
Sixteen milliseconds.
So we know that the call to request animation frame is going to be then it's 16 milliseconds.
So if we now try this out with this call to take, we should expect the test to be passing and going
back here to our test results.
We can see that that is indeed the case.
Now calling here TEQ 16 requires internal knowledge about how the component that we are testing is implemented.
So I would not read the test this way instead of a simple call to flesh will ensure that all the tasks
in the main test.
Q And also in the micro tasks.
Q are getting emptied.
So at this point in the test, we are sure that we can write our assertions now in order to test a synchronous
functionality.
I would recommend that you use the fake async zone whenever possible because you get the most flexibility
and because you can write synchronous looking tests that are easy to maintain and reasoned about.
Now, there are some particular cases where it's not possible to use the fake async zone.
This should be very rare.
And also we can see that there is here in the before each block here, we have here a call to a sync.
So async is another angle of testing utility for writing.


CYPRESS:
1)	Installing cypres:      Npm install  --dev cypress
2)	Launching cypress in open mode: npm run cypress:open
Deployment:
•	Ng test  --watch=false –code-coverage
We are going to head over to the command line and we're going to run the following command engy tests,
just like we do before we are going to add the flag minus minus watch.
And we are going to set it to false, meaning that our tests are not going to be run in what mode.
Instead, this is going to be a single execution run where all the tests are going to get executed and
then the angular clay is going to exit.
Now, in order to trigger the cloud cover as a report, we're going to add the flag minus minus code
coverage.

EPA server:
Npm install -g http-server

I recommend that you install globally the EDP server by using the following commands, NPM install minus
G, HTP Desh server.
And this is going to give us a good command line utility server order to run this new folder that was
generated.

Run this 
http-server -c -1 .

This is going to disable all caching headers.
And let's add here the dot, meaning that we want to serve the content of the current folder.
This is then going to start a new server on Port Eighty-eight.


Calling Production:
In package.json add this line
“build:prod”:”ng build --prod”
In cmd run :
ng build –prod
Now, in order to create a production build, we are going to call the command and build with the option
minus minus prob.
Let's try this out to see how this works.
We're going to go to the command line and we're going to run NPM Run, build Callon Broad.
This is going to take a moment, but at the end it should have a DCED folder containing the productionversion of our application.


Run in projection mode:
In package.json add
“start:prod”:”http-server ./dist -prod 4200”
In cmd run 
Npm run start:prod

Run in cypressmode:
In package.json add
“cypress:run”:”cypress run”
In cmd run 
Npm run cypress:run 


Running multiple tests in sequence:
In package.json add
“build-and-deploy:prod”:”run-s build:prod start:prod”,
“e2e”:”start-server-and-test build-and-deploy:prod http://localhost:4200 cypress:run”
In cmd run 
Npm run e2e
e2e=end to end



Running Cypress E2E Tests using Travis CI:

The below command auto generates video animation in deployement
npm run cypress:run 
