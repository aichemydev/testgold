Github Actions with the TestGold Interceptor 
============================================================================

We can integrate directly with your existing test assets in a Github repository using github actions. 
This gives you flexibility to run tests automaticaly when you commit any changes. To set up a github action, you can follow a few simple steps:

1: If you do not already have any github actions setup in your repository, create a folder titled: "./github/workflows". This lets Github know that you are using a Github action.
Within this folder, you can create a yml file based on this base template. This

.. code-block::


    name: TestGold CI Testing

    on:
    push:
        branches:
        - master
    pull_request:
    

    jobs:
    build:
        env:
        PY_COLORS: "1"
        runs-on: ubuntu-18.04
        strategy:
        fail-fast: false
        max-parallel: 6
        matrix:
            python-version: [3.6, 3.7, 3.8, 3.9]

        steps:
        - uses: actions/checkout@v1
        - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v1
        with:
            python-version: ${{ matrix.python-version }}
        - name: Preparing Environment
        run: |
            rm selenium-20.11.0-py2.py3-none-any.whl
        continue-on-error: true
        - name: Download TestGold Interceptor
        run: |
            wget https://dev.testgold.dev/api/interceptor/download/selenium-20.11.0-py2.py3-none-any.whl
        - name: Install TestGold Interceptor
        run: |
            pip install selenium-20.11.0-py2.py3-none-any.whl
        - name: Install dependencies
        run: |
            python -m pip install --upgrade pip
            cd ./python_scripts/
            pip install -r requirements.txt
        continue-on-error: true
        - name: Install Chrome and Firefox
        run: |
            sudo apt install google-chrome-stable
            sudo apt-get install firefox
        - name: Setup Interceptor Options and Run
        # Add Your TG_TOKEN as a secret for your github repo      
        # https://docs.github.com/en/actions/security-guides/encrypted-secrets     
        run: |
            export TG_ANALYZER=1 
            export TG_TOKEN=${{ secrets.TG_TOKEN }} 
            python ./python_scripts/realworldapp_test.py


This sample will download the TestGold interceptor to your GitHub Actions container allowing you to utilize the features of the TestGold platform. To adapt this sample to your use case a couple things need to be modified. Please

2: To begin modifications to this yml fine to suit your specific repo configuration, change the path to your projects requirements if certain python packages are needed to run your tests. This can be done by modifying the line to point to the appropriate requirments location: 

.. code-block::

    pip install -r requirements.txt

3: Now you are ready to configure the interceptor to run your tests. You can chose to enable the analyzer using the following command line:

.. code-block::

    export TG_ANALYZER=1

You can set this equal to 0 to diable the analyzer.

4: You will then need to provide your TG_TOKEN. The token can be found in the installation tab of the TestGold Site. Next once you have this, our reccomendations will be to add this to your repositories secrets under the name TG_TOKEN. Keep in mind that you will need to update the secrets when the token has been refreshed. 

.. code-block::

    export TG_TOKEN=${{ secrets.TG_TOKEN }} 

This snippet shows you how to access your TG_TOKEN from the repository secrets. Now you are ready to use the python command to run any of your python test scripts via the TestGold Interceptor.
You can view results from your tests on the TestGold Site.