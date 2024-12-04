---
title: 'SSH keys'
description:
  'SSH keys are a pair of cryptographic keys used for secure communication and
  authentication purposes in the context of SSH (Secure Shell) protocols. They
  ensure secure access to remote servers and systems by establishing a secure
  and encrypted connection over an insecure network. An SSH key pair consists of
  two components:'
---

# SSH keys

## Definition

SSH keys are a pair of cryptographic keys used for secure communication and
authentication purposes in the context of SSH (Secure Shell) protocols. They
ensure secure access to remote servers and systems by establishing a secure and
encrypted connection over an insecure network. An SSH key pair consists of two
components:

1. Public key: This is the key that is safely shared and can be freely
   distributed to any remote system the user wishes to access. It is used to
   encrypt messages that only its corresponding private key can decrypt.

2. Private key: This key remains confidential and is kept secure by the user. It
   is used to decrypt messages encrypted by the matching public key and to
   authenticate the user to the remote system.

The use of SSH keys eliminates the need for passwords, significantly reducing
the risk of brute force attacks and other common security vulnerabilities
associated with password-based authentication. They are commonly used by system
administrators and by individuals for secure file transfers, remote system
maintenance, and automated processes.
