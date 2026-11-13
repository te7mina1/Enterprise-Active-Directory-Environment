# Lab-04-Service-Accounts-and-SPN-Experiments

Service identities and Service Principal Name (SPN) exercises in the `allsafe.local` lab.

## Overview

This lab documents an SPN registration and lookup exercise involving the lab account `SQLService`. The screenshots show an SPN entry being written to Active Directory and then appearing in a domain SPN query. They do not establish that a SQL service is running under that account or that Kerberos authentication succeeds.

## Objectives

- Document the intended service identity and its relationship to an SPN.
- Record the SPN registration and lookup evidence.
- Check whether the recorded SPN matches the actual service, host, and port.
- Identify the validation and credential-hygiene work required before calling the exercise complete.

## Lab Environment

| Component | Value |
|---|---|
| Domain | `allsafe.local` |
| Domain Controller | `AllSafeCS-DC01` — `192.168.56.10` |
| Service account | `SQLService` (shown under the domain `Users` container) |
| Recorded service port | `60111` (verify against the actual SQL service configuration) |
| Tools | Active Directory Users and Computers; Windows PowerShell `setspn` |

## Techniques and Tools

- Active Directory service identity and SPN review
- `setspn` registration and domain SPN lookup in the isolated lab
- Microsoft guidance for SQL Server SPN naming and duplicate-aware registration

## Methodology

1. Identified the lab directory account named `SQLService` as the intended service identity; the notes associate it with port `60111`.
2. Recorded an SPN registration attempt using `setspn -a`. The screenshot shows an “Updated object” response for the `SQLService` directory object.
3. Queried the lab domain's SPNs. The result displayed the recorded entry under the `SQL Service` object and reported “Existing SPN found!”.
4. Compared the value shown in the screenshot with the SQL Server SPN format and marked the account-to-service mapping, hostname, and port for verification.

## Findings

- The recorded SPN is `ALLSAFECS-DC01/SQLService.ALLSAFE.local:60111`.
- The query output shows this value associated with the `SQL Service` object in `allsafe.local`; that confirms the directory query returned the entry, not that SQL Server is using it or Kerberos authentication works.
- The value shown does not match the usual SQL Server TCP SPN pattern `MSSQLSvc/server-name.domain:port`. Confirm the actual SQL service host, service account, and listening port before registering or changing an SPN. [Microsoft: Register a Service Principal Name for Kerberos Connections](https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections?view=sql-server-ver17)
- The screenshots document use of `setspn -a`. For any corrected registration, use the duplicate-checking registration option documented by Microsoft, and do not remove or replace an existing SPN until the service mapping is confirmed. [Microsoft: setspn](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/setspn)
- No service-start, Kerberos authentication, duplicate-check, or corrected-SPN evidence is recorded here. Keep the exercise in progress until those checks are captured.
- Passwords from the source identity notes are deliberately omitted. Remove plaintext lab passwords from the notes and rotate any that are still in use before sharing the project.

## Screenshots

Only the two images corresponding to the SPN registration and domain SPN lookup are included in [Lab-04-Service-Accounts-and-SPN-Experiments-Lab-Shots](./Lab-Shots)

## Lessons Learned

- An SPN must describe the real service and be registered on the account that runs it.
- A successful directory update or a query match is not proof that the service is configured correctly or that Kerberos works.
- Verify the hostname, service identity, port, and duplicates before making further changes.
- Keep credentials out of documentation and public repositories.

## Conclusion

The lab records an SPN registration attempt and a query that found the entry. The SPN format and actual SQL service mapping still need validation, so this remains an in-progress exercise rather than a verified Kerberos configuration.
