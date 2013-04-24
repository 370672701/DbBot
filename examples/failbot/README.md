FailBot
=======

FailBot is a Python script used to produce a summary web page about the most failing
suites, tests and keywords, using the information stored in a DbBot database.

Please adjust (the barebone) HTML templates in 'failbot/templates' to your needs.


Requirements
------------
* Python 2.6 or newer installed
* DbBot

Tested and verified on Python 2.7.4.


Usage
-----
The executable is 'failbot' in directory 'bin'.

You need to append the DbBot root path to your PYTHONPATH,
because some of the DbBot's packages are used by FailBot.

So running the script from command-line:

    PYTHONPATH=/path/to/DbBot bin/failbot [options]

Required options are:

Short format    | Long format             | Description
--------------- |-------------------------| ------------------------------------------
-o              | --output                 | Output HTML file name

Additional options are:

Short format    | Long format             | Description
--------------- |-------------------------| ------------------------------------------
-v              | --verbose               | Be verbose about the operation
-b DB_FILE_PATH | --database=DB_FILE_PATH | SQLite database of test run results (robot_results.db by default)

On Windows environments, you might need to rename the executable to have the '.py' file extension
('failbot' -> 'failbot.py').


Usage examples
--------------

Please make sure that you append the DbBot root path to your PYTHONPATH.
Otherwise you will end up getting errors like this:

    Traceback (most recent call last):
      File "bin/failbot", line 7, in <module>
        from failbot import DatabaseReader, HtmlWriter, WriterOptions
      File "/something/FailBot/failbot/__init__.py", line 4, in <module>
        from .database_reader import DatabaseReader
      File "/something/FailBot/failbot/database_reader.py", line 3, in <module>
        from dbbot import RobotDatabase
    ImportError: No module named dbbot

So please issue this command (if using Bash) before running failbot:

    export PYTHONPATH=$PYTHONPATH:/path/to/DbBot

You may also want to add this line to your .bash_profile to avoid running
the command in every new shell.

The output HTML filename is always required:

    failbot -o index.html

You might want to create the output somewhere under your public_html:

    failbot -o /home/<username>/public_html/index.html

If -b/--database is not specified, a database file 'robot_results.db' is used by default.

With a non-default named database:

    failbot -f atest/testdata/one_suite/output.xml -b my_own_database.db


Directory structure
-------------------

Directory | Description
----------|------------
bin       | Contains the executable. You may want to append this directory to your PATH.
templates | HTML templates used to produced the summary page.
failbot   | Contains the packages internally used by failbot.
