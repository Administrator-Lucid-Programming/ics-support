# ICS Pro Activation Transfer and Deactivation Policy

Effective September 23, 2026

## Scope

An individual ICS Pro license is assigned to one person. Each supported editor
installation counts as an activation, including separate supported editors on
the same machine. The number of simultaneous activations and any additional
transfer or reset rights are those stated at purchase. This policy explains how
the extension manages an activation; it does not increase the activation
allowance purchased.

## Transferring an activation

To move an activation to another machine:

1. On the currently activated machine, run **ICS: Deactivate License**.
2. Wait for confirmation that deactivation succeeded.
3. On the destination machine, run **ICS: Enter License Key** and enter the
   same key.

The extension removes its local license key, instance record, and validation
cache only after Lemon Squeezy confirms deactivation. This releases the old
machine's activation before the destination machine requests a new one.

## Changing the key on one machine

Only one saved ICS Pro license is managed on a machine at a time. If a license
is already saved, **ICS: Enter License Key** accepts that same key for
validation but refuses a different key. Run **ICS: Deactivate License** first,
wait for confirmation, and then enter the different key.

This rule prevents an old remote activation from being abandoned when its
local key and instance identifier are overwritten.

## Failed deactivation

If Lemon Squeezy rejects the request or cannot be reached, the extension keeps
the local license key, instance record, and cache. The activation has not been
confirmed as released, so retry **ICS: Deactivate License** when service is
available. The extension does not present local deletion as successful remote
deactivation.

Uninstalling the extension or deleting its local data does not send a
deactivation request and may leave the machine counted against the activation
limit.

## Machine unavailable

If the activated machine has been lost, replaced, or cannot run the extension,
use the private merchant-support route shown on the Lemon Squeezy order page or
receipt to request an activation reset. Whether a reset is available is governed
by the purchase terms. Do not publish a license key, order details, or customer
information in the public issue tracker.

## Privacy

Activation, validation, and deactivation use Lemon Squeezy as described in the
[Privacy Notice](./PRIVACY.md). Source code and generated output are not sent as
part of these license operations.
