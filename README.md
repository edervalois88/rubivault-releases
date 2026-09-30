# RubiVault · pilot builds

This repository holds nothing but the pilot builds of RubiVault for Windows and the document an
installed copy updates itself from. The product's source lives in a private repository.

## Install

1. Trust the pilot certificate once, on the machine that will run RubiVault. It is a self-signed
   certificate, so Windows needs it in **both** the root and the trusted-people store of the
   machine, which is why this step asks for an administrator:

   ```powershell
   Import-Certificate -FilePath .\rubivault-pilot.cer -CertStoreLocation Cert:\LocalMachine\Root
   Import-Certificate -FilePath .\rubivault-pilot.cer -CertStoreLocation Cert:\LocalMachine\TrustedPeople
   ```

2. Install from the installer document, which is what makes the following builds arrive on their
   own:

   `RubiVault-staging.appinstaller`

   Or install the package once by hand:

   ```powershell
   Add-AppxPackage -Path .\RubiVault-staging-<version>-win-x64.msix
   ```

The package installs per user and never asks for an administrator. Only the certificate step does,
and only once per machine.

## What is in each release

| File | What it is |
| --- | --- |
| `RubiVault-staging-<version>-win-x64.msix` | The application and its native agent, signed |
| `RubiVault-staging.appinstaller` | The document an installed copy updates itself from |
| `rubivault-pilot.cer` | The public half of the signing certificate. It can verify a signature and cannot make one |

Each build points at `app.rubivault.com`. Installing a newer package over an older one works
without uninstalling anything first.
