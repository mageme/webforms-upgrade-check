# WebForms 4 upgrade check

One file that tells a store running MageMe WebForms 3.x whether it is ready for the upgrade to
WebForms 4. Run it **before** `composer update`. It does not load Magento and changes nothing in the
store; it works on PHP 7.4 and later.

## Download and check

```bash
curl -fsSLO https://github.com/mageme/webforms-upgrade-check/releases/latest/download/wf4-readiness.php
curl -fsSLO https://github.com/mageme/webforms-upgrade-check/releases/latest/download/wf4-readiness.php.sha256
sha256sum -c wf4-readiness.php.sha256
```

## Run

```bash
php wf4-readiness.php [<magento-root>] [--json]
```

Without a path it checks the current folder, so run it from the Magento root. The first line shows
the version of the check; `--version` prints only that, `--help` prints the usage.
`--acknowledge-print-templates` is still accepted and changes nothing: a custom print template is reported as a
warning and does not block the upgrade.

| Exit code | Meaning |
|---|---|
| 0 | Ready |
| 1 | Blocking findings — fix them first |
| 2 | The check could not finish: the path is not a Magento root, or the data checks were skipped (no database in `app/etc/env.php`, the database unreachable, a query failed) |

Each release here matches a WebForms 4 release of the same version. The upgrade itself is described
at https://docs.mageme.com.
