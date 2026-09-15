# Changes to DEBIAN11-CIS-Audit

## Aug26 Updates

### Benchmark alignment to v2.0.0

- Renumbered System Auditing tests from 6.3.x to 6.4.x to match the benchmark - directories,
  filenames, titles, CIS_ID metadata, rule gates, vars/CIS.yml and goss.yml
- Corrected the 6.4.4.1 to 6.4.4.4 off-by-one - log file mode, owner and group owner now sit on
  6.4.4.1, 6.4.4.2 and 6.4.4.3, and the log directory mode test on 6.4.4.4
- Corrected the 7.2.5 to 7.2.9 off-by-one - duplicate UID, GID, user name and group name tests
  now match their control, and 7.2.9 tests home directories
- cis_6.4.4.7.yml checked file owner instead of group - now uses stat %G
- cis_5.3.3.3.3.yml was a duplicate of 5.3.3.3.2 - retitled and regated to 5.3.3.3.3
- Corrected rule gates that referenced the wrong toggle in cis_1.1.2.6.4.yml, cis_1.1.2.7.4.yml,
  cis_2.3.3.2.yml and cis_7.1.6.yml
- Added missing tests for 1.5.5, 5.4.2.8, 6.1.3 and 7.2.10
- Split cis_1.6.1_6.yml into cis_1.6.1.yml through cis_1.6.6.yml so 1.6.4, 1.6.5 and 1.6.6 gate
  on their own toggles instead of 1.6.1, 1.6.2 and 1.6.3
- Level gates and server/workstation metadata aligned to Profile Applicability in 16 test files
- cis_1.4.1.yml tested /boot/grub/grub.conf - corrected to grub.cfg
- cis_1.7.10.yml tested /etc/gdm/custom.conf - corrected to /etc/gdm3/custom.conf
- Titles corrected for 1.4.2, 6.4.1.1, 6.4.2.4, 6.4.3.6 and 6.4.3.7
- Added deb11cis_rule_1_5_5, deb11cis_rule_6_1_3 and deb11cis_apport_mask to vars/CIS.yml
- Corrected stale section numbers in vars/CIS.yml comments
- README updates and updated contributing and contributors

### QA pass

- 7.2.4 was a byte-for-byte copy of the 7.2.5 duplicate-UID test and reused its resource key
  no_dup_uid. Goss overwrites duplicate keys on load, so 7.2.4 was silently dropped from every
  run. Replaced with a real shadow-group-empty check
- 5.4.2.8 used bash process substitution and 5.4.1.6 used a bash [[ ]] test. Goss runs commands
  under sh, which is dash on Debian, so both failed to parse, produced no output and always
  reported compliant. Rewritten POSIX-safe. 5.4.1.6 also asserted on "Failure" while the script
  echoes "failure"
- 1.6.1, 1.6.2 and 1.6.3 carried an unterminated regex '!/[Ll]inux' which goss treats as a
  literal substring, so the OS-leak check never fired. Terminated
- Anchored config-file patterns in 1.3.1.2, 5.1.7, 5.1.14, 5.1.16, 6.2.1.2.2 and the 19 fstab
  persistence checks. Without a start anchor a commented-out line satisfied the test
- Added the missing timeout to the 6.2.2.1 recursive find
- Document markers added or corrected in 4 test files
- CONTRIBUTING.md header corrected to Ansible-Lockdown Projects
- goss documentation links aligned with the other audit repos
- .gitignore now carries the secrets and QA artifact patterns it was missing
- 3.1.2 asserted that modprobe blacklist entries exist whether or not the host has wireless
  hardware, so it always failed on hardware without it while remediation correctly did nothing.
  Replaced with the interface-aware check used by the other Debian audit repos
- 2.3.2.1 built its NTP pattern with a leading space after the "=", so it could never match what
  the remediation template writes
- 6.4.3.9 looked for `-F key=perm_mod` while the rules template writes `-k perm_mod`, and used
  one b32 chown syscall order for both the rules file and `auditctl -l`. The kernel normalises
  the live order differently, so each resource now carries the order its own source produces

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
