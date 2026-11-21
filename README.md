# Operation: Silent Night

USS Rhode Island Blue Crew family holiday hub. The website runs on GitHub Pages; Google Apps Script receives greetings into a private Google Drive folder. The site does not require the organizer's computer or ChatGPT to stay open.

## Features

- Christmas countdown at 7:40 a.m. America/New_York time.
- Drive-hosted news video, animated Santa sonar, holiday radio, and submarine trivia.
- Private video greeting uploads, with 15-second and 25 MB limits in the visitor form.
- A server-controlled Christmas landing-video release. The landing video and family submissions remain private in Drive.
- No IndexedDB, localStorage, Firebase, or browser-only submission vault.

## Cloud configuration

The Apps Script project uses the Advanced Drive v3 service. Its manifest requests the per-file `drive.file` permission plus `script.external_request` for retrieving the app's private landing video from Google's Drive API. It does not request full-Drive access.

Deploy the final `Code.gs` plus the `UPLOAD_HTML_` string generated from `Upload.html` as an Apps Script web app, executing as its owner and accessible to visitors. Run storage initialization once in the editor before deploying. The initialization helper must not be exposed as a public web-app function.

Script properties:

| Property | Value |
| --- | --- |
| GREETING_FOLDER_ID | Folder created by the uploader during initialization |
| LANDING_VIDEO_ID | Private landing-video file created through the app's own uploader |
| RELEASE_AT | `2026-12-25T07:40:00-05:00` |

The website's upload iframe and landing iframe use the deployed Apps Script URL. Private uploads never go into the public GitHub repository. The greeting API provides upload receipts but no public listing or download operation. File names and video contents stay in the organizer's private Drive.

## Validation

Run `node --test tests/upload.test.cjs` from the source project. The checks cover validation failures, private file creation, duplicate retries, daily quotas, release-time boundaries, source syntax, and absence of browser persistence. Live browser and Drive tests must also be completed during deployment.

The public news video is viewable by link for embedding. The landing video is retrieved by the server only after the release time. The Santa tracker is fictional entertainment.
