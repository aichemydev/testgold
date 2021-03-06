Release Notes
=============

The notes below indicate what has changed with each release of our platform.

Next release
------------

- Test scripts can be now be run and healed in your own test environment, using
  our downloadable Selenium Interceptor packages for Javascript, Java, and
  Python. See :doc:`Using our Selenium Interceptor externally <./externaluse>`
  for details.

- CSS selectors are now supported, enabling heal and suggest processing of
  Selenium's ``findElement(By.CSS_SELECTOR)``, ``findElement(By.CLASS_NAME)``,
  ``findElement(By.NAME)``, and ``findElement(By.ID)``.

- Initial support for Appium selector healing.


2020-09-21
------------

- Generic archive files (tarballs, zip files, etc.) can now be uploaded as a
  test dependency. These will be unpacked in the test run directory to make
  their contents available for your test scripts.

- Performance improvements for complex websites.

2020-09-16
----------

- Typescript is now supported. Typescript tests must be in the form of valid NPM
  packages.

- Direct uploads of test scripts or packages are now supported.

2020-09-09
----------

- We now support adding dependencies for test scripts. This is enabled for
  Javascript and Python test scripts for the moment. Java support will come
  later.

- Tests can now be run using Python and Javascript packages. For Python, we
  accept packages in the following formats: .whl, .tar.gz, .zip. For Javascript,
  we accept NPM packages in the following formats: .tar.gz, .tgz.

2020-09-02
----------

- Current release only supports xpath locator healing, CSS and more will be
  supported in a later release.

- Only single files are supported for Python and Javascript, more will be
  supported in the near future.

- Files need to be uploaded or updated with Github URL and token, we are adding
  more enterprise configuration options in the near future.
