# ICS Language Tools Privacy Notice

Effective September 15, 2026

## Summary

ICS Language Tools performs source conversion and language processing locally.
The extension does not intentionally transmit source code, filenames, project
paths, editor contents, ICS output, or generated C# to Lucid Programming or
Lemon Squeezy.

The extension does not include its own analytics or usage telemetry.

Local server-latency diagnostics retain aggregate request counts, outcomes and
timings in memory. The optional Start/Finish Server Latency Measurement commands
produce a local report without source text, paths or request parameters. These
measurements and reports are not uploaded automatically.

## Runtime installation

ICS depends on Microsoft's .NET Install Tool extension to install and maintain
the user-level .NET 10 runtime used by the bundled converter. The Install Tool may
contact Microsoft services to locate, download, and update that runtime. ICS
passes it the requested runtime version and mode and the ICS extension ID; ICS
does not pass source code, filenames, project paths, editor contents, ICS
output, generated C#, or license data to the Install Tool. Microsoft's
extension, services, settings, and privacy terms govern that installation.

## License activation and validation

Network access to `https://api.lemonsqueezy.com` occurs only for ICS Pro license
activation, periodic validation, and user-requested deactivation.

During activation, the extension sends:

- the license key entered by the user; and
- VS Code's machine identifier as the Lemon Squeezy instance name.

During later validation, the extension sends:

- the license key; and
- the instance identifier returned by Lemon Squeezy during activation.

During deactivation, the extension sends the same license key and instance
identifier. After Lemon Squeezy confirms deactivation, the extension deletes
the locally stored license key, instance state, and validation cache. If
deactivation fails, that local data is retained so the request can be retried.
Uninstalling the extension or deleting its local data does not itself send a
deactivation request to Lemon Squeezy.

VS Code describes its machine identifier as a unique identifier for the
computer. As with any Internet request, Lemon Squeezy may also receive ordinary
connection and request metadata, such as an IP address and HTTP headers, under
its own privacy terms.

Lemon Squeezy's response may contain license, product, order, instance, or
customer metadata. The extension uses the activation or validation result,
license status and expiry, instance identifier, error message, and the numeric
store and product identifiers needed to confirm that the key belongs to ICS Pro.
It does not retain customer or order metadata from the response.

## Data stored locally

The extension stores:

- the raw license key in VS Code Secret Storage;
- a SHA-256 hash of the key for cache invalidation;
- the Lemon Squeezy instance identifier;
- the VS Code machine identifier; and
- cached validation status, timestamps, expiry, the trusted numeric store and
  product identifiers, and the most recent validation message.

A successful validation is cached for no more than 30 days and never beyond a
known earlier license expiration date.

This information is used only to activate, validate, deactivate, and cache ICS
Pro access. It remains under VS Code's local extension-storage mechanisms until
successful deactivation or removal through VS Code's storage or extension-data
controls. Local removal alone may leave the remote activation active.

Preview editing also stores recovery snapshots in the extension's local storage.
These snapshots contain the source path, C# and ICS text, and the last synchronized
text pair; they can therefore contain sensitive source code. They are not uploaded
or placed in the source tree. The active recovery copy is removed when the paired
C# has been synchronized and saved. Each window also maintains its own latest
snapshot per source, preventing another window from overwriting the only copy.
Saving synchronized C# retires that window's snapshot; snapshots from other or
previous sessions remain for manual recovery. Explicit conflict resolution and
preview reversion also retain backups until you remove them. Use **ICS: Open Preview
Recovery Folder** to inspect or delete these files. The files are not encrypted by
ICS and rely on your operating system's account and storage protections.

## User-initiated bug reports

When an ICS operation fails, the extension may offer **Report Issue**. The same
action is available from the Command Palette and control panel. Choosing it
prepares a diagnostic report in an untitled local editor. The report is not
included in a URL and is not transmitted to GitHub automatically.

The report contains product and environment versions plus redacted error and
stack information. Automated redaction cannot guarantee that arbitrary error
text contains no project identifiers or source fragments, so the extension
requires the user to review the local report before offering to copy it and
open the public GitHub issue form. The user must paste and submit the report
deliberately. GitHub processes the resulting visit and anything the user pastes
or submits under GitHub's own terms and privacy notice.

## Checkout and external pages

Choosing **ICS: Upgrade to Pro** opens the configured purchase page in the
default browser. The website and payment provider process that visit under
their own terms and privacy notices. ICS Language Tools does not receive
payment-card details.

## Other software

VS Code, the operating system, Git hosting providers, and other installed
extensions may independently process data. Their behavior is outside this
notice and is governed by their respective settings and privacy terms.

## Changes

This notice may be updated when the extension's data practices change. Material
changes will be reflected in the notice distributed with a later release.
