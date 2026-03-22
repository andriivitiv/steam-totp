# steam-totp

[![Test](https://github.com/andriivitiv/steam-totp/workflows/Test/badge.svg)](https://github.com/CyberAndrii/steam-totp/actions)
[![License: MIT](https://img.shields.io/github/license/andriivitiv/steam-totp?label=License)](LICENSE)

A GitHub Action for generating Steam two-factor authentication (TOTP) codes. Useful for automating workflows that require Steam login, such as SteamCMD.

# Usage

Example of logging into SteamCMD within a workflow:

```yaml
steps:
- name: Setup steamcmd
  uses: andriivitiv/setup-steamcmd@v1
  
- name: Generate auth code
  id: steam_totp
  uses: andriivitiv/steam-totp@v1
  with:
    shared_secret: ${{ secrets.STEAM_SHARED_SECRET }}
  
- run: steamcmd +login ${{ secrets.STEAM_USERNAME }} ${{ secrets.STEAM_PASSWORD }} ${{ steps.steam_totp.outputs.code }} +quit
```

This action is commonly used alongside [setup-steamcmd](https://github.com/andriivitiv/setup-steamcmd).
 
# Inputs

| name          | description                                                      | required | default |
|---------------|------------------------------------------------------------------|----------|---------|
| shared_secret | Shared secret from the `.maFile`.                                | true     |         |
| time_offset   | Offset (in seconds) added to the current time before generation. | false    | 0       |

# Outputs

| name | description                |
|------|----------------------------|
| code | Generated Steam TOTP code. |
