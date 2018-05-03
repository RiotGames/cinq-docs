.. _local-development:

Standalone Local Development Environment Setup Script
=====================================================

Note: The instructions here are **NOT** for production. They are strictly for local development.

Introduction
------------

This script is written to meet the need for people who

* Would like to (or have to) develop in VM
* Want to setup the environment in a simple and straight forward approach

Requirements
------------

* Ubuntu 16.04 or higher (We tested this script on Ubuntu 16.04.4 x64)
* Internet Access
* Be able to ``sudo``

How to use this script
----------------------

1. Save ``https://raw.githubusercontent.com/RiotGames/cloud-inquisitor/localdev/packer/scripts/setup_localdev.sh`` to the host you want to use as the dev instance.
2. Go to the directory where the script is saved, ``chmod +x ./setup_localdev.sh`` then ``sudo ./setup_localdev.sh``.
3. Wait till the script finishes.
4. Setup your AWS credentials (Optional. See section below)
5. Run ``/proj/cinq-dev/bin/cloud-inquisitor runserver`` and save the admin credential in the output. You will need this to login the user interface.
6. Now you have a working local dev instance for Cinq development. The project will be saved under ``/proj`` with its virtualenv located at ``/proj/cinq-dev``

Set up your AWS credentials
---------------------------

You have 2 approaches to setup your AWS credentials

Option 1: Open ``~/.cinq/config.json`` and fill the fields below. Note if you are not using temporary credentials, the `session_token` row needs to be deleted:

::

    {
        ...

        "aws_api": {
            "instance_role_arn": "FILL_INSTANCE_ROLE_ARN",
            "access_key": "YOUR_AWS_ACCESS_KEY",
            "secret_key": "YOUR_AWS_SECRET_ACCESS_KEY",
            "session_token": "YOUR_AWS_SESSION_TOKEN"
        },

        ...
    }

Option 2: Same as Option 1, but don't fill `access_key`, `secret_key` and `session_token`. Instead, you put your credentials at places where will be looked up by `boto3` library. (http://boto3.readthedocs.io/en/latest/guide/configuration.html#configuring-credentials)

Notes
-----

Below are things you might need to pay attention to

* We don't recommend running the script directly under root.
* You probably need to set the working directory to ``/proj`` if you plan to use an IDE to do the development
* If you'd like to develop other plugins, you need to ``git clone`` them to ``/proj``, ``chdir`` to where ``setup.py`` is located, then ``/proj/cinq-dev/bin/pip3 install -e .``
