# FileRise: path traversal in trash restore

https://github.com/error311/FileRise/security/advisories/GHSA-2qx7-5r33-3hhj

FileRise is a self-hosted PHP file manager (error311/FileRise). I reviewed v3.24.0, commit `765eccc`, and reported this on 2026-07-31 through GitHub private vulnerability reporting. The vendor published it on 2026-08-12. Fixed in 3.25.0. No CVE has been assigned.

Restoring a trashed file does not keep the destination inside storage. `FileModel::restoreFiles()` trusts the stored path too far. On its own, a restore is an administrator action. I also had a separate upload bug, published as GHSA-5gg8-vgm3-x4fj, that lets a low-privileged user place the bad entry. If an administrator later restores it, the result is code execution. The vendor treated those as two advisories and scored this one for the combined case.

My first scores were 9.0 and then 8.8 and 8.2, with scope changed. Those were wrong. Scope stays on the application. The numbers we agreed:

| Reading | Vector | Score |
|---|---|---|
| Published advisory. Low-privileged user plants the entry, an administrator restores it. | CVSS:3.1/AV:N/AC:L/PR:L/UI:R/S:U/C:H/I:H/A:H | 8.0 High |
| Restore taken alone. Administrator only, no click from a second person. | CVSS:3.1/AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H | 7.2 High |

| | |
|---|---|
| Affected | 3.7.0 ≤ version < 3.25.0 |
| Fixed | 3.25.0 |
| CWE | CWE-22, CWE-434, CWE-829 |
| CVE | Not assigned |

The vendor set 3.7.0 as the earliest confirmed release from the imported history, rather than claiming every older tag. I agreed. 3.25.0 fixes the restore. I retested it. Deleting a file and restoring it puts the file back where it was. The traversal does not.

They said a CVE would be requested through the GitHub advisory after the bounds were settled, and asked me not to request one separately. I did not. As of 2026-09-22 there is still no CVE id on the advisory.

Local Docker only, `error311/filerise-docker` at v3.24.0, then v3.25.0 for the fix. No other deployment.

L0stHeart
https://github.com/L0stHeart
