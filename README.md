# flutter-tizen-action
GitHub actions support for flutter-tizen. Build and sign a tpk in one step.

### Prerequisites

Make sure you have these packages intalled:

`package-manager-cli.bin install --accept-license NativeCLI NativeToolchain-Gcc-9.2 Certificate-Manager cert-add-on`

[Also do this](https://docs.tizen.org/application/dotnet/tutorials/certificates/creating-certificates/)

MAKE SURE YOUR PASSWORDS CAN BE PARSED IN THE COMMAND LINE WITHOUT QUOTES

### Usage

Action:

```
build_tpk:
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v1
      with:
        dotnet-version: '5.0.x'
    - uses: Rexios80/flutter-tizen-action@v4
      with:
        author-certificate-file: author.p12
        author-certificate-password: hunter2
        distributor-certificate-file: distributor.p12
        distributor-certificate-password: hunter3

    - name: Archive artifact
      uses: actions/upload-artifact@v2
      with:
        name: tpk
        path: build/tizen/tpk/*.tpk
```

Inputs:

```
project-root:
  description: 'The root of your flutter-tizen project'
  required: false
  default: $GITHUB_WORKSPACE
tizen-studio-version:
  description: 'Tizen Studio version (default 4.1)'
  required: false
  default: '4.1'
tizen-platform:
  description: 'The platform your app runs on'
  required: false
  default: 'WEARABLE-5.5'
author-certificate-file:
  description: 'Author certificate file'
  required: true
author-certificate-password:
  description: 'Author certificate password'
  required: true
distributor-certificate-file:
  description: 'Distributor certificate file'
  required: true
distributor-certificate-password:
  description: 'Distributor certificate password'
  required: true
```
