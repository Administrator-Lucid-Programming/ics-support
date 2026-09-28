# Privacy notice — ICS for Visual Studio

Last updated: 28 September 2026

ICS conversion, diagnostics, formatting, live projections, recovery snapshots,
and conflict backups run locally. The extension does not intentionally transmit
source code, filenames, project paths, generated C#, diagnostics, recovery data,
or issue reports to Lucid Programming or any other service. It contains no Lucid
analytics or usage telemetry.

## License operations

ICS Pro activation, validation, and user-requested deactivation contact
`api.lemonsqueezy.com`. Activation sends the license key and a pseudonymous
instance name derived from the Windows machine identifier. Validation and
deactivation send the license key and Lemon Squeezy activation instance ID.
No source code or project information is included.

Validation can run automatically during extension initialization or a Pro-access
check when there is no valid cached result. If a saved key lacks a matching
instance record, that check can reactivate it. These requests do not require you
to invoke **ICS: Refresh License** manually.

The raw license key is encrypted for the current Windows user with DPAPI. The
extension stores only activation metadata, a hash of the key, the expected
product/store identifiers, and a time-limited validation cache in its local
application-data directory. Successful deactivation removes the local key,
instance record, and cache after Lemon Squeezy releases the activation.

## Local recovery data

Dirty ICS projections, conflict backups, and locally prepared issue reports may
contain source code. They are stored only under the current user's local
application-data directory. Conflict backups are removed after 30 days and are
also limited to the newest 20 complete C#/ICS pairs and normally 100 MB; the
newest pair is retained even if it alone exceeds that size. Unrestorable drafts
are removed when detected. Use **ICS: Open Preview Recovery Folder** to inspect
the files or **ICS: Clear Preview Recovery Data** to delete all drafts and
conflict backups after confirmation. Nothing in that folder is uploaded
automatically.

**ICS: Report Issue** opens a scrubbed report locally. You decide whether to copy
any content to the public issue tracker. Review it first and do not submit
proprietary code, license keys, paths, customer information, or other sensitive
data.

Visual Studio, Windows, Git hosting providers, and other installed extensions may
process data independently under their own terms.
