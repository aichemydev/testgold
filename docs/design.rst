Philosophy and Design
=====================

We believe Selenium is a great open platform for testing software.
However, testing software with Selenium has lead people to constantly rewrite and maintain their tests to keep up with development cycles.

Unfortunately, due to these struggles, we now require two teams of coders - a set of developers and a set of testers.
The testers have to keep updating their selenium scripts to match the pace of developers. This leads to a cat and mouse catchup game for testers worldwide.

Instead of allowing QA teams freedom and flexibility to improve coverage and predict user behavior, modern QA teams are
simply verifying that yesterday's changes did not break core functionality. They are re-checking that login, search, and a few key flows from yesterday's new build
did not break their selenium tests. Furthermore, in the likely case that it did break their selenium tests, QA engineers will rewrite the tests, update page object models,
fix locator and object detectors, improve timeouts, and then commit these into the repository. There is full knowledge that this process will rinse and repeat.

QA managers have told us that during key releases, rewriting selenium tests can easily take more than 95% of the time consumed by QA engineers.
QA managers have told us that instead of spending time on rewriting selenium, they would like them to:

1. Improve scenario and test coverage by 5-10x
2. Enable faster release cycles to the customer
3. Allow enterprises to issue bug fixes quickly to affected customers

As a counter to efficient testing, we hear of lax stories of A/B testing from some teams at Facebook. The claim is you don't need to test software as much,
and can fix customer reported bugs quickly. That's great if you are Facebook, and are serving social media consumers,
but what if you are serving critical enterprise applications. Enterprise solutions have a lot of competition, for cost, customer support, and feature velocity.
Can you afford a lax attitude for testing?

Our solution is a method that empowers QA, removes their drudgery with maintenance of tests to move on to the higher value problems that software managers are looking for.

By supporting selenium interception on various languages, Java, Python, Javascript, and even the Selenium IDE, our aim is to make maintenance painless while letting QA focus on more interesting challenges.
