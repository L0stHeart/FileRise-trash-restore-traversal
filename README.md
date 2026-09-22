# FileRise: path traversal in trash restore

https://github.com/error311/FileRise/security/advisories/GHSA-2qx7-5r33-3hhj

Affects FileRise 3.7.0 up to, but not including, 3.25.0. Fixed in 3.25.0.

High. CVSS:3.1/AV:N/AC:L/PR:L/UI:R/S:U/C:H/I:H/A:H (8.0).
CWE-22, CWE-434, CWE-829.
No CVE assigned.

Restoring from trash does not keep the destination inside storage. On its own, that restore is an administrator action. Scored alone, with high privileges and no user interaction, it is 7.2. The published 8.0 is the case that also uses a separate upload bug: a low-privileged user plants the entry, and an administrator restores it later. The vendor confirmed both readings. 3.25.0 fixes the restore.

Reported 2026-07-31 through GitHub private vulnerability reporting. The vendor published the advisory on 2026-08-12.

L0stHeart
