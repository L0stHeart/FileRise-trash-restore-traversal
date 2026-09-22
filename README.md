# FileRise trash restore does not stay inside storage

https://github.com/error311/FileRise/security/advisories/GHSA-2qx7-5r33-3hhj

Severity: high. No CVE. CWE-22, CWE-434, CWE-829.

FileRise 3.7.0 up to but not including 3.25.0 is affected. Fixed in 3.25.0. The vendor took 3.7.0 as the earliest release they would confirm from the imported history.

`restoreFiles()` trusts the stored path too far, so a restore can land outside storage. Taken alone, that restore is an administrator action. Scored that way it is 7.2 (`CVSS:3.1/AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H`). The published advisory is the other reading, 8.0 (`CVSS:3.1/AV:N/AC:L/PR:L/UI:R/S:U/C:H/I:H/A:H`): a low-privileged user plants the entry using the separate upload bug [GHSA-5gg8-vgm3-x4fj](https://github.com/error311/FileRise/security/advisories/GHSA-5gg8-vgm3-x4fj), and an administrator restores it later. That case reaches code execution. The vendor kept the two bugs on separate advisories. They do not share a fix.

My earlier scores were 9.0, then 8.8 and 8.2, all with scope changed. Scope stays on the application. 8.0 and 7.2 are the numbers we agreed.

3.25.0 fixes the restore. I retested it. Deleting a file and restoring it puts the file back where it was. The traversal does not. The vendor was going to request the CVE from GitHub and asked me not to file one elsewhere. I did not. As of 22 September 2026 there is still no CVE id.

Local Docker only, `error311/filerise-docker` at v3.24.0 (commit 765eccc) and again at v3.25.0.

Reported privately on 31 July 2026. The vendor published the advisory on 12 August 2026.

L0stHeart
