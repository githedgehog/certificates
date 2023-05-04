# Hedgehog Certificates

These are all certificates that are used in our SONiC and ONIE software builds.
For the time being we publish both our production as well as test certificates to the same repository.
All files that have `-prod-` in them belong to certificates that are being used in release builds (tagged builds).
All files that have `-test-` in them are included in development builds only (and therefore of no real use for the general public tbh).
All certificates are being offered in PEM and DER encoded formats purely for convenience reasons, so that there is no need for manual conversions between the formats depending on the use-case.

Below is a section for every use-case and a description of all certificates and their purpose.

## Secure Boot

These are all certificates which are used for our for trusted UEFI Secure Boot chain.

- `sb-microsoft-test-1.der` - This is the authority which is used in our development QEMU images. It acts as the authority which is signing our TEST shim binaries. This allows us to properly test Secure Boot without the need of enrolling MOKs. There is obviously no production/release equivalent. The release equivalent is Microsoft.

- `sb-shim-prod-1.der` - This is the `Hedgehog Secure Boot CA` authority which is signing our GRUB bootloader release builds as well as the release ONIE and SONiC Linux kernels. Its certificate is embedded in our shim release builds which gets signed by Microsoft.
- `sb-shim-test-1.der` - This is the `Hedgehog Secure Boot TEST CA` authority which is signing our GRUB bootloader development builds as well as the development ONIE and SONiC Linux kernels. Its certificate is embedded in our shim development builds which gets signed the the authority in `sb-microsoft-test-1.der`.

- `sb-grub-pgp-prod-1.der` - This is the `Hedgehog GRUB Signer CA` authority which is actually a PGP key. It is used to sign all GRUB configuration files as well as everything that GRUB is loading. Its key is embedded in the GRUB binaries. This is technically not part of UEFI Secure Boot but an enhancement for Secure Boot disallowing unintended GRUB scripts from running. The concept is inherited from ONIE.
- `sb-grub-pgp-test-1.der` - This is the `

## Kernel Modules

For both SONiC and ONIE builds we are including the following certificate authorities into the Linux kernel.
Both Hedgehog SONiC and ONIE kernels require modules to be signed.
Therefore they must be signed by either our RSA or EC DSA certificate authorities.
Even though technically ONIE does not ship with kernel modules, ONIE would load modules that were signed with either of these authorities.

- `kernel-ecdsa-prod-1` - This is the `Hedgehog Kernel Module Signer ECDSA CA` authority. It signs kernel modules with ECDSA signatures as they could be included in production/release builds.
- `kernel-ecdsa-test-1` - This is the `Hedgehog Kernel Module Signer ECDSA TEST CA` authority. It signs kernel modules with ECDSA signatures as they could be included in development builds.
- `kernel-rsa-prod-1` - This is the `Hedgehog Kernel Module Signer RSA CA` authority. It signs kernel modules with RSA signatures as they could be included in production/release builds.
- `kernel-rsa-test-1` - This is the `Hedgehog Kernel Module Signer RSA TEST CA` authority. It signs kernel modules with RSA signatures as they could be included in development builds.

## OCI Artifacts

We are using [cosign](https://github.com/sigstore/cosign) to sign all of our OCI artifacts that ship with the control node appliance (seeder) images.
The certificates here represent the signing authority that signed all OCI artifacts as they are present in the image registry in the appliance.

- `cosign-prod-1` - This is the `Hedgehog OCI Artifacts Signer CA` authority. It signs all OCI artifacts as they are included in release builds.
- `cosign-test-1` - This is the `Hedgehog OCI Artifacts Signer TEST CA` authority. It signs all OCI artifacts as they are included in development builds.
