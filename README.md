Demonstrate a bug: tox-gh-actions won't run a tox environment if it isn't mentioned in the tox `envlist` setting.

The tox.ini here has 3.7 and 3.9 in the envlist. The envlist is used as the default if nothing is specified:

```
$ tox -q
RUNNING TOX!
Python 3.7.8
RUNNING TOX!
Python 3.9.0
______________________________ summary _______________________________
  py37: commands succeeded
  py39: commands succeeded
  congratulations :)
```

Even without 3.8 in the envlist, tox will run a 3.8 environment if asked:

```
$ tox -q -e py38
RUNNING TOX!
Python 3.8.6
______________________________ summary _______________________________
  py38: commands succeeded
  congratulations :)

$ TOXENV=py38 tox -q
RUNNING TOX!
Python 3.8.6
______________________________ summary _______________________________
  py38: commands succeeded
  congratulations :)

```

But tox-gh-actions won't run py38, even with it configured in the `[gh-actions]` section of tox.ini.  It will only run py38 if it is added to `envlist`.
