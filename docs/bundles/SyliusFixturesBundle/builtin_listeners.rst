Built-in listeners
==================

**SyliusFixturesBundle** comes with a few useful listeners.

Logger (``logger``)
-------------------

Provides output while running ``sylius:fixtures:load`` command.

.. code-block:: bash

    # Without logger

    $ app/console sylius:fixtures:load my_suite
    $ _

    # With logger

    $ app/console sylius:fixtures:load my_suite
    Running suite "my_suite"...
    Running fixture "country"...
    Running fixture "locale"...
    Running fixture "currency"...
    $ _

The logger does not have any configuration options. It can be enabled in such a way:

.. code-block:: yaml

    sylius_fixtures:
        suites:
            my_suite:
                listeners:
                    logger: ~

ORM Purger (``orm_purger``)
---------------------------

Purges the relational database. Uses ``delete`` purge mode and the default entity manager if not configured otherwise.

Configuration options:

    - ``purge_mode`` - sets how databse is purged, available values: ``delete`` (default), ``truncate``
    - ``managers`` - an array of entity managers' names used to purge the database, ``[null]`` by default

Example configuration:

.. code-block:: yaml

    sylius_fixtures:
        suites:
            my_suite:
                listeners:
                    orm_purger:
                        purge_mode: truncate
                        managers:
                            - custom_manager

PHPCR / MongoDB Purger (``phpcr_purger`` / ``mongodb_purger``)
--------------------------------------------------------------

Purges the document database. Uses the default document manager if not configured otherwise.

Configuration options:

    - ``managers`` - an array of document managers' names used to purge the database, ``[null]`` by default

Example configuration:

.. code-block:: yaml

    sylius_fixtures:
        suites:
            my_suite:
                listeners:
                    phpcr_purger:
                        managers:
                            - custom_manager # Uses custom document manager
                    mongodb_purger: ~ # Uses default document manager
