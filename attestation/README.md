# Attestation Certificates

This folder contains attestation certificates which prove that the keys for all the certificates in this repository were generated on a YubiHSM hardware device.
We do not have our own attestation certificate infrastructure and simply rely on the builtin attestation certificate/key from Yubico.
Download their [intermediate certificate](https://developers.yubico.com/YubiHSM2/Concepts/E45DA5F361B091B30D8F2C6FA040DB6FEF57918E.pem) and [root CA certificate](https://developers.yubico.com/YubiHSM2/Concepts/yubihsm2-attest-ca-crt.pem) to be able to verify the attestation trust chain for any certificate in this repository.
