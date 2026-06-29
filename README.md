# uBlock-Origin-Lite-ADMX-Templates

Community ADMX/ADML templates for configuring uBlock Origin Lite with Microsoft Edge and Google Chrome Group Policy.

The templates expose the managed settings documented by the uBlock Origin Lite project in the Windows Group Policy editor.

Official documentation:  
https://github.com/uBlockOrigin/uBOL-home/wiki/Managed-settings

This is not an official uBlock Origin Lite project and is not affiliated with uBlock Origin, Raymond Hill, Microsoft, or Google.

## Included files

```text
PolicyDefinitions/uBlockOriginLite.admx
PolicyDefinitions/de-DE/uBlockOriginLite.adml
PolicyDefinitions/en-US/uBlockOriginLite.adml
```

## Supported browsers

```text
Microsoft Edge: cimighlppcgcoapaliogpjjdehbnofhn
Google Chrome:  ddkjiahejlhfcafbddmgiahcphecmpfh
```

The templates configure uBlock Origin Lite settings only. They do not install the extension. Extension installation has to be configured separately with the browser extension policies.

## Available settings

- `defaultFiltering`
- `disabledFeatures`
- `disableFirstRunPage`
- `noFiltering`
- `popupBlockMode`
- `rulesets`
- `showBlockedCount`
- `strictBlockMode`

## Installation

Copy the ADMX/ADML files into your Group Policy Central Store:

```text
\\example.com\SYSVOL\example.com\Policies\PolicyDefinitions\uBlockOriginLite.admx
\\example.com\SYSVOL\example.com\Policies\PolicyDefinitions\de-DE\uBlockOriginLite.adml
\\example.com\SYSVOL\example.com\Policies\PolicyDefinitions\en-US\uBlockOriginLite.adml
```

Close and reopen the Group Policy Management Console.

The policies should appear under:

```text
Computer Configuration or User Configuration
  Administrative Templates
    uBlock Origin Lite
      Microsoft Edge
      Google Chrome
```

## Example configuration

A simple Edge baseline could look like this:

```text
Default filtering mode:       optimal
Disable first-run page:       Enabled
Popup blocking:               Enabled
Show blocked count:           Enabled
Strict blocking:              Enabled
No filtering:                 ["example.com", "mycorp.test"]
Rulesets:                     ["+default", "+adguard-spyware-url", "+annoyances-cookies"]
Disabled features:            ["dashboard"]
```

The example rulesets keep the default rulesets enabled and add URL tracking protection plus cookie notice filtering.

Do not add `filteringMode` to `disabledFeatures` if users should be able to set individual websites to "No filtering" when troubleshooting broken pages.

## JSON values

The following settings expect single-line JSON arrays:

- `disabledFeatures`
- `noFiltering`
- `rulesets`

Example:

```json
["example.com", "mycorp.test"]
```

## Verify on a client

After applying Group Policy, restart the browser and check:

```text
edge://policy
chrome://policy
```

You can also check the registry.

Microsoft Edge:

```powershell
Get-ItemProperty 'HKLM:\Software\Policies\Microsoft\Edge\3rdparty\extensions\cimighlppcgcoapaliogpjjdehbnofhn\policy'
```

Google Chrome:

```powershell
Get-ItemProperty 'HKLM:\Software\Policies\Google\Chrome\3rdparty\extensions\ddkjiahejlhfcafbddmgiahcphecmpfh\policy'
```
