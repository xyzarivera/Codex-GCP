# Cloud Key Management Service

## Overview

- manage cryptographic keys for every service within GCP
- keys in encryption
  - at rest
  - in transit
- default, created in KMS, uploaded in KMS
- generate, use, rotate, destroy symmetric keys
- automatic or at-will key rotation
- support asymmetric keys
- integrated with Cloud IAM and Cloud Audit Logs
- Permissions are handled by Access Control Lists (ACLs) on a per key basis
  - per key policy
- Used with Cloud HSM
- DEKs are encrypted with a key encryption key (KEK)
- process known as envelope encryption
  - encrypting key with another key
- central repository for storing KEKs
- KEKs not exportable from KMS
- Automatically rotates KEKs at regular intervals
- Standard rotation period is 90 days

## Avaialbility

- Regional - zone
- Dual Regional - zones in 2 specific geographical places
- Multi Regional
- Global
- Read operatons re served by a datacenter close to the requesting user or service
- Write oprations mus propagate to multiple data centers hwen performed on multi-regional or global resources - will be slower as a result

## Object Heirarchy

Keys are stored in a heirarchical structure

- Project
  - KMS belong to a projec
  - best practice is to run in a separate project
- Location 
  - where KMS keys are stored
  - were KMS receives requests
- Key Ring 
  - grouping of keys for organizational purposes
  - Keys inherit permissions from the key ring
- Key
  - Cryptographic key
  - Symmetric or asymmetric
- Key Version
  - Materiail that makes up the key (length, algorithm)
  - Numbered sequentially
  - states: enabled, disabled, scheduled for destruction, or destroyed
    - any version can be used for decrption until that version is disabled, scheduled for destruction, or destroyed

## Key States

- Pending Generation
  - asymmetric keys only
- Enabled
- Disabled
  - key material still available
  - can be still enabled
- Scheduled for destruction
  - can be put back to disabled state
- Destroyed
  - no longer stored in KMS
  - not recoverable
- Symmetric Encryption
  - primary key version to be enabled for encryption
- Asymmetric Encryption
  - key version to be enabled for encryption or digital signing

## Key Rotation

- Symmetric Key Rotation
  - A new key version of a key is generated
    - new key marked as primary
    - previous key not destroyed
      - available for decryption
  - Automatic Key rotation
- Asymmetric key rotation
  - a new key version of a key is generation
  - manual key rotation only
    - because consists of private-public key pair

When a symmetric key is used for encryption or decryption, the user specifies a key, not a key version. KMS handles te encryption and decryption usage on behalf of theh user when a symmetric key is rotated.

## Cloud KMS

### Separaion of Duties

- ensuring that one individual does not have all necessary permissions
- users normally should not have access to decryption keys
- Move KMS to its own project

### Secret Management

- Cloud KMS does not directly store secrets
- encrypts secrets that you store elsewhere
- Use default encryption built into Cloud Storage buckets
- use application layer encryption using ag key in Cloud KMS

## Resources

[acloudguru](https://acloudguru.com/)
