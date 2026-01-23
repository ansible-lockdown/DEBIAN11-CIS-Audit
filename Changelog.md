# Changes to DEBIAN11-CIS-Audit

## 2.0.0

- 2.0.0 Updates from 2026_Jan_Updates

### YAML Lint Fixes

- Added document start `---` to `vars/CIS.yml` and `goss.yml`
- Fixed indentation for `deb11cis_time_servers` list in `vars/CIS.yml`
- Fixed comment indentation in `goss.yml` for section headers
- Replaced non-breaking spaces with regular spaces in comments
- Added `.yamllint` configuration to handle Jinja2 template syntax

### Spelling/Grammar Corrections in vars/CIS.yml

- Fixed "controling" to "controlling" (line 123)
- Fixed "IPv5" to "IPv6" (line 232)
- Fixed "This are" to "These are" (line 293)
- Fixed section comment "5.4.2" to "5.4.3" (line 319)
- Fixed "choses" to "chooses" (line 500)
- Added missing space in "`chrony`and" (line 501)
- Removed duplicate "of" in "list of of" (lines 505, 512)
- Fixed "managaed" to "managed" (line 532)
- Fixed "dependancy" to "dependency" (line 536)
- Fixed "seperated" to "separated" (line 615)

## 0.2 updates

Several control updates and new tests
adopted new goss binary >= 0.4.0 now required

## 0.1 initial release

- Based on CIS 1.0
