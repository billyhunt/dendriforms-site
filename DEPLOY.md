# Deploy dendriforms.ai

This file explains how the site is published. It is written for a person or an
agent with no other context.

## What this is

- A one-page static site for Dendriforms. All files are in this folder. There
  is no build step.
- The contact form posts to Web3Forms. Its access key is the `access_key` field
  in `index.html`.

## How it is published (since 2026-11-26)

- Pushing to `main` publishes the site. `.github/workflows/deploy.yml` signs in
  to the Dendriforms AWS account (372620611633) with GitHub's OpenID Connect
  token, copies the files to the S3 bucket and clears the CloudFront cache. No
  AWS keys are stored in GitHub.
- The workflow reads three repo variables: `AWS_ROLE_ARN`, `SITE_BUCKET` and
  `DISTRIBUTION_ID`. Their values come from `ql output dendriforms-ai`.
- It skips `.git`, `.github` and Markdown files.
- The hosting itself (bucket, CloudFront, certificate, DNS records, publish
  role) is defined in <https://github.com/Dendriforms/quicklaunch>, in
  `deployments/dendriforms-ai`. Change it there, never in the AWS console.
- `www.dendriforms.ai` redirects to `dendriforms.ai`.

## Domain and DNS

- `dendriforms.ai` is registered at DreamHost. Its name servers point at the
  Route 53 zone in the Dendriforms AWS account.
- Every record lives in Route 53 and is managed by Terraform in the quicklaunch
  repo (`terraform/bootstrap`): Google mail (`MX`), the Google site verification
  (`TXT`), the email-sending records for `noreply@dendriforms.ai`, and the site
  records. Do not add records at DreamHost; DreamHost no longer answers for the
  domain.

## History

- Until 2026-11-21 the old site ran on AWS Amplify with no reachable source.
- 2026-11-21 to 2026-11-26: GitHub Pages served this repo.
- 2026-11-26: moved to the Dendriforms AWS account, and GitHub Pages was turned
  off.

## The access key

If the Web3Forms key is lost, get a new one at <https://web3forms.com>. Enter the
email address that must receive the messages. The key arrives by email. The key
is safe to publish: it can only send mail to that address.

Do not put an email address on the page. The owner does not want one there.

## Test after a change

1. Open <https://dendriforms.ai> and <https://www.dendriforms.ai>. Both must
   show the site.
2. Open the site on a phone.
3. Send one test message through the form. Confirm that it arrives by email.
4. Select "Start a project" at the top. It must jump to the form.

## If spam arrives

The form has a hidden honeypot field (`botcheck`). It stops simple bots only.
Web3Forms recommends hCaptcha for stronger protection. Its documentation shows
how to add it:
<https://docs.web3forms.com/getting-started/customizations/spam-protection/hcaptcha>

hCaptcha adds a visible widget and an outside script. Add it only if spam is a
problem.

## Design notes, for later changes

- The look is a quiet relative of the Alethia design system
  (<https://github.com/billyhunt/design-systems>, `systems/alethia`).
- Colours: paper `#f2f0eb`, ink `#111111`, muted `#5f5c55`, hot `#ff3b00`.
- The logo is a small tree of straight lines: a trunk, two right-angle
  branches and three squares. It sits before the wordmark and is also the
  favicon. The logo never changes.
- Larger trees can grow. Where there is room (the back of the business card,
  for example), a tree can have more branches. Every tree follows four rules:
  straight lines only, right-angle branches, a square at the end of each
  branch, and one orange square at the top.
- The underline on "works." covers the word only, not the full stop.
- The hot colour appears four times only: the top square of the tree mark, the
  underline on "works.", and the two buttons. Keep it rare.
- Type: Archivo 600 for headlines in sentence case, Archivo 400 for text,
  DM Mono capitals for small labels, Archivo Black for the wordmark only.
- Corners are square. Rules are 2 px or 3 px. No shadows, no gradients.
- Fonts are hosted with the site. Do not load fonts from the network.
- The copy presents Dendriforms as a team ("we"). No clients are named.
