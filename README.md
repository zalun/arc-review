## Wrapper around Phabricator's `arc` cli to support submission of a series of commits.


### Goals

- must only use standard libraries
- must be a single file for easy deployment
- should work on python 2.7 and python 3.5+

### Configuration

`review` has an INI style configuration file to control defaults: `~/.review-config`

This file will be created if it doesn't exist.

```
[ui]
no_ansi = False

[submit]
auto_submit = False
always_blocking = False

[updater]
last_check = <time>
```

- `ui.no_ansi` : never use ANSI colours (default: auto-detected).
- `submit.auto_submit` : when true the confirmation prompt will be skipped
    (default: false).
- `submit.always_blocking` : when true reviewers in commit descriptions will be marked
    as blocking. reviewers specified on the command line override this setting
    (default: false).
- `updater.last_check` : epoch timestamp (local timezone) indicating the last time
    an update check was performed.

`review` can also be configured via the following environmental variables:
- `IS_DEV` : connect to phabricator dev instance (default: connect to production)
- `DEBUG` : enabled debugging output (default: disabled)
- `UPDATE_FILE` : when self-updating write to this file instead of __file__

e.g. To enable debugging output on MacOS/Linux:
```
  $ DEBUG=1 review submit
```
