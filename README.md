# PhimHay – QA Test Documentation

Test documentation for **PhimHay**, an online movie website (ASP.NET Core MVC, .NET 8, EF Core, SQL Server). I wrote it as a QA practice exercise: a test plan, 74 test cases, and 9 bug reports, all based on running the application myself.

> **Note:** PhimHay is a school project (source code: [KhietLoi/PhimHay](https://github.com/KhietLoi/PhimHay)). No testing was done during development, and the bugs below have not been fixed, so all of them are still in **Open** status.

## Results at a glance

| Metric | Result |
|---|---|
| Test cases designed | 74 across 17 feature areas |
| Executed | 74 of 74 |
| Passed / Failed / Blocked | 63 / 9 / 2 |
| Pass rate (of executed) | 85.1% |
| Bugs reported | 9 (3 High, 4 Medium, 2 Low) |

## What is in this repository

**[`PhimHay_Test_Documentation.xlsx`](PhimHay_Test_Documentation.xlsx)** has four sheets:

| Sheet | Contents |
|---|---|
| **Summary** | Totals, pass rate, bug counts, and main risks. Calculated with formulas from the other sheets. |
| **Test Plan** | Scope, test types, techniques, environment, entry/exit criteria, and risks. |
| **Test Cases** | 74 cases with module, priority, preconditions, steps, test data, expected and actual result, status, and linked bug ID. |
| **Bug Reports** | 9 bugs with steps to reproduce, expected vs. actual result, severity, environment, and evidence. |

Bug evidence (screenshots) is stored in a [shared Google Drive folder](https://drive.google.com/drive/folders/1T3lKjPBsFDNd3v29SjTyNb19VlDfphjC?usp=drive_link).

## Approach

- **Scope:** registration, email verification, login/logout, password reset and change, profile, authorization, movie list, filter, search, pagination, watch page, comments, ratings, favorites, watch history, and admin management.
- **Test types:** functional, negative/validation, authorization (access control), basic UI/usability
- **Techniques:** equivalence partitioning, boundary value analysis, and error guessing. For example, password length 7 vs. 8, and page numbers 0, −1, and 9999.
- **Expected results:** there was no requirements document, so I derived expected behavior from the controllers and models. Where the code behavior looked wrong, I logged a bug instead of changing the expected result.
- **Out of scope:** performance and load testing, security penetration testing, and automated tests.
- **Environment:** Windows 10, run locally with .NET SDK 8.0 and SQL Server, tested in Chrome and Edge on desktop.

## Test coverage

| Area | Cases | Area | Cases |
|---|---|---|---|
| Registration | 10 | Movie detail | 4 |
| Login | 8 | Comments | 4 |
| Password | 7 | Rating | 3 |
| Search | 6 | Movie list | 3 |
| Authorization | 5 | Filter | 3 |
| Admin – movies | 5 | Favorites | 2 |
| Email verification | 4 | Admin – users | 2 |
| Profile | 4 | Admin – content | 2 |
| UI / Compatibility | 2 | | |

## Bugs found

| ID | Title | Severity |
|---|---|---|
| BUG05 | Guest (not logged in) can open the Admin dashboard directly | **High** |
| BUG06 | Normal user can open Admin pages directly (no role check) | **High** |
| BUG07 | Invalid page number in the URL crashes the site with an unhandled exception | **High** |
| BUG02 | Invalid email format is rejected with no error message shown | Medium |
| BUG04 | Reset password: wrong or missing minimum-length message, and weaker rules than registration | Medium |
| BUG08 | Search does not match Vietnamese text typed without diacritics (e.g. "An do" vs. "Ấn Độ") | Medium |
| BUG09 | Home page carousel buttons overlap the movie's play button | Medium |
| BUG01 | Special-character password check does not accept `-` or `_`, and the message does not list allowed characters | Low |
| BUG03 | Reusing a verification link shows "invalid link" instead of "already verified" | Low |

### Most important finding

**BUG05 / BUG06:** the Admin area has no authorization check. Any visitor, logged in or not, can open `/Admin` directly by URL and see admin data and management functions. This should be fixed before any real deployment.

## Notes on test results

- 2 cases are marked **Blocked** because the behavior does not apply in this app: TC33 (file type is already filtered before upload) and TC44 (combined filter and sort is not supported).
- The pass rate is calculated as Passed ÷ Executed.

## Author

**Nguyễn Vũ Thanh Liêm**
Email: [luci.gh.itch.io@gmail.com](mailto:luci.gh.itch.io@gmail.com)
