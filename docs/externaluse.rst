Using the TestGold Interceptor externally
=========================================

We now support direct calls to our healing API from Selenium tests running
outside of our own service. For this purpose, we have released Selenium packages
for Java, Javascript, and Python that interface with our API and obtain healed
XPaths for web automation tests that run in your own environment. These
*TestGold Interceptor* packages can be used in place of the usual Selenium
packages to take advantage of our API.

To download these packages, contact `support@testgold.dev
<mailto:support@testgold.dev>`_. You will be pointed to a page that hosts these
packages after you sign up for an account.

.. image:: _static/interceptor-download.png
   :width: 100%
   :align: center
   :alt: Interceptor download page

Using the Interceptor packages
------------------------------

A single environment variable is required for the Interceptor packages to
interface with our API. Set the **TESTGOLD_AIO_TOKEN** as directed on the
download page, then install one of the Interceptor packages.

- **Java**: Download the Interceptor package JAR and replace any references to
  the usual Selenium JAR in your test classpaths with this JAR.

- **Javascipt**: Download the Interceptor package and install it using NPM:
  ``npm install <interceptor-package-name>.tgz``. This will override your usual
  Selenium NPM dependency automatically.

- **Python**: Download the Interceptor package and install it using pip:
  ``pip install <interceptor-package-name>.whl``. This will override your usual
  Selenium Python package dependency automatically.

Run your Selenium tests as normal, making sure the **TESTGOLD_AIO_TOKEN**
environment variable is set. The Interceptor will log its actions and the
results of the XPath healing process to the terminal console. It will also
provide a **results URL** where you can browse the results of each XPath
encounter and the outcomes of the healing process.

Customizing Interceptor execution
---------------------------------

You may set the following environment variables to customize how the Interceptor
package and our API heals your tests:

- **USE_INTERCEPTOR**: This is set to '1' by default. Set this to '0' to make
  the Interceptor package behave exactly like normal Selenium, with no calls to
  the TestGold API for healing broken XPaths.

- **WAL_SERVER_TIMEOUT**: Sets how long to wait for each broken XPath to be
  healed by the TestGold API. Most heals are complete within 30 seconds for
  uncomplicated web pages, but highly complex web pages may take several minutes
  for the TestGold API to return a result for broken XPaths. This is set to 10
  minutes by default.

- **INTERCEPTOR_FILTER_DISPLAYED**: This is set to '0' by default. If set to '1',
  only currently displayed elements will be used to generate a snapshot of the
  current state of a web page for the TestGold API instead of all elements. This
  can greatly speed up processing for a highly complex web page.

- **INTERCEPTOR_FILTER_DISPLAYED**: This is set to '0' by default. If set to '1',
  only currently enabled elements will be used to generate a snapshot of the
  current state of a web page for the TestGold API instead of all elements. This
  can greatly speed up processing for a highly complex web page.

- **INTERCEPTOR_HANDLE_FAILURE**: If this is set to 'suggest-xpaths' (default),
  broken XPaths that are untrained (they were not uploaded to the TestGold API
  for training our learning algorithms before) will not immediately fail. The
  TestGold API will instead attempt to heal them in-place, and suggest
  alternative XPaths that may select the element that was intended to be
  selected. This is not as powerful as our usual XPath healing engine, but
  provides a reasonable fall-back option if all you have is a broken XPath and
  no way to get to the initial known-good state of an XPath and Selenium tests.

- **INTERCEPTOR_FAST_HEAL**: Every time the TestGold Interceptor encounters an
  XPath and the resulting element selection is successful, it collects
  information on the element and the current state of the web page to send to
  the TestGold API for training our healing engine. This extra work can
  sometimes slow down your tests. If you've already run a training session on
  web page for our API or you are sure that the state of a currently broken web
  page has not changed between your test runs, set this environment variable to
  '1' to skip this information collection and assume that the page has not
  changed in state between the current run and any previous runs of the
  Interceptor.

  This variable is set to '0' by default to ensure the TestGold API always is
  up-to-date on the latest state of the web page under test. Note that if the
  TestGold API detects that the web page contents have changed since its last
  snapshot of the web page, it will not send stale healing results, in which the
  Interceptor will automatically collect all the required information to
  snapshot the current state of the web page and send it to the API.

- **INTERCEPTOR_RESULT_JSON**: if this environment variable is set, it should
  point to a .json file on disk where the results for successful XPath heals and
  suggestions from the TestGold API will be saved. The file name will be
  prefixed with the test run request ID as assigned by the TestGold API.

- **INTERCEPTOR_LOG_LEVEL**: Set to one of '1' (debug), '2' (info, default), '3'
  (warning), or '4' (error). This affects the verbosity of the Interceptor
  logging.
