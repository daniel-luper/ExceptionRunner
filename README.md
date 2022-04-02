Tasks to answer in your own README.md that you submit on Canvas:

1.  See logger.log, why is it different from the log to console?
    
The output to logger.log is different from that in the console because we specified in logger config file (logger.properties) that the log file handler should display all levels of log messages whereas the log console handler should only display info messages and above.

2.  Where does this line come from? FINER org.junit.jupiter.engine.execution.ConditionEvaluator logResult Evaluation of condition [org.junit.jupiter.engine.extension.DisabledCondition] resulted in: ConditionEvaluationResult [enabled = true, reason = '@Disabled is not present']

It comes from JUnit, specifically an internal function called "logResult" that gets called by Assertions.assertTrue.

3.  What does Assertions.assertThrows do?

Assertions.assertThrows executes the given Executable (in this case, a lambda). If the Executable throws an 
exception of the given type, then the assertion passes. Otherwise, the assertion fails, causing the
entire test to fail.

4.  See TimerException and there are 3 questions
    1.  What is serialVersionUID and why do we need it? (please read on Internet) -> serialVersionUID is "an identifier that is used to serialize/deserialize an object of a Serializable class" (Baeldung.com). We need it because an Exception is a Serializable, and we want to distinguish it from other kinds of Exceptions.
    2.  Why do we need to override constructors? -> If we don't override the constructors, we won't be able to pass arguments into the exception's constructor. We typically want to be able to specify a description message for the exception and sometimes give another exception as the cause as well. Only the default constructor (no parameters) gets auto-generated by Java. 
    3.  Why we did not override other Exception methods? -> We didn't override other Exception methods because the Exception class is designed so that you typically don't need to do so--the default behavior is usually already great.
5.  The Timer.java has a static block static {}, what does it do? (determine when called by debugger)

The Timer.java static block gets called at the start of the program; it tries to open the log config file, load the config, and log an initial info message.

6.  What is README.md file format how is it related to bitbucket? (https://confluence.atlassian.com/bitbucketserver/markdown-syntax-guide-776639995.html)

It is called "Markdown", it lets devs easily format text for writing README files and PR descriptions and comments.
Bitbucket is configured to display the formatted text automatically for maximum eye candy!

7.  Why is the test failing? what do we need to change in Timer? (fix that all tests pass and describe the issue)

The test is failing because the wait time given is negative, which causes the method to throw a TimerException, but the start time has not been initialized yet. This means that whenever we try to log the time difference (end - start), we get a NullPointerException because we're trying to do an operation on the null starting time value. The test fails because a NullPointerException gets thrown, but such an Exception was not expected by the JUnit test. 

8.  What is the actual issue here, what is the sequence of Exceptions and handlers (debug)

Tester.timeMe throws a TimerException which causes the finally block in Timer.timeMe to execute. Then, a NullPointerException gets thrown during the subtraction and gets caught by the JUnit assertThrows method. Finally, an AssertionFailedError gets thrown which is what actually causes the test to fail.

9.  Make a printScreen of your eclipse JUnit5 plugin run (JUnit window at the bottom panel) 

See ./junit.png

10.  Make a printScreen of your eclipse Maven test run, with console

See ./maven.png

11.  What category of Exceptions is TimerException and what is NullPointerException

TimerException is a checked exception and NullPointerException is an unchecked exception.

12.  Push the updated/fixed source code to your own repository.

Ok