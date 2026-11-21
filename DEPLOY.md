# Deploy dendriforms.ai

This file lists every step to put the site live. It is written for a person or
an agent with no other context.

## What this is

- A one-page static site for Dendriforms. It is a placeholder site.
- All files are in this folder. There is no build step.
- The page works as it is. The contact form's Web3Forms access key is in
  `index.html` (step 1 is done).

## Current state (2026-11-21)

- Domain: `dendriforms.ai`, registered at DreamHost.
- The old site ran on AWS Amplify. Its source repo could not be found. Before
  this change, DNS had no `A`, `ALIAS` or `CNAME` records for `@` or `www`, so
  the old site was already unreachable. `MX` (Google) and `TXT` records remain.
- The old site used Web3Forms for its contact form.
- Repo: <https://github.com/billyhunt/dendriforms-site>. GitHub Pages serves
  `main` from the root folder (steps 2 and 3 are done).
- The GitHub Pages `A` and `CNAME` records were added at DreamHost through the
  DreamHost API, and HTTPS is enforced (steps 4 and 5 are done).

## Target

GitHub Pages, from a new public repo, with the custom domain `dendriforms.ai`.
It is free and needs no AWS account.

## Steps

### 1. Add the Web3Forms access key (done)

The key is the `access_key` field in the form in `index.html`. To change it,
replace that value.

If the old key is lost, get a new one at <https://web3forms.com>. Enter the
email address that must receive the messages. The key arrives by email. The
key is safe to publish: it can only send mail to that address.

Do not put an email address on the page. The owner does not want one there.

### 2. Create the repo and push

1. Create a public repo, for example `billyhunt/dendriforms-site`. Leave it
   empty.
2. Put all files from this folder in the repo root. Keep `CNAME` and
   `.nojekyll`.
3. Commit and push to `main`.

Free GitHub Pages needs a public repo.

### 3. Turn on GitHub Pages

1. In the repo: Settings, then Pages.
2. Source: "Deploy from a branch". Branch: `main`, folder `/ (root)`.
3. Custom domain: `dendriforms.ai`. The `CNAME` file sets this already. Confirm
   that the field shows it.

### 4. Change DNS at DreamHost

Use the records that GitHub shows in its Pages documentation. Confirm them
there before you change anything:
<https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site>

At the time of writing, the records are:

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `billyhunt.github.io` |

If any old records for `@` or `www` that point at AWS Amplify have come back,
remove them. Do not remove mail (`MX`) or `TXT` records.

DNS changes can take up to a day. They are usually faster.

### 5. Turn on HTTPS

1. Go back to Settings, then Pages.
2. Wait until the DNS check passes.
3. Select "Enforce HTTPS".

### 6. Test

1. Open <https://dendriforms.ai> and <https://www.dendriforms.ai>. Both must
   show the new site.
2. Open the site on a phone.
3. Send one test message through the form. Confirm that it arrives by email.
4. Select "Start a project" at the top. It must jump to the form.

### 7. Remove the old site

When the new site is live and the form works, delete the old Amplify app in the
AWS console. This stops the AWS charges for it.

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
