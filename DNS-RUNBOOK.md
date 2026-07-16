# DNS runbook: pointing wholeyield.com at GitHub Pages

**You have to do this part yourself.** It needs your Namecheap login, which I do
not have and should not have.

Everything below was checked against live DNS on 2026-07-15.

---

## READ THIS FIRST: two ways to break your email

Your domain has no website today, but it **does** run your Google Workspace
email (danielh@wholeyield.com). The mail depends on records that live in the
same DNS panel you are about to edit.

### 1. Do not touch the MX records

These five are live right now and are what deliver your mail:

```
1   aspmx.l.google.com
5   alt1.aspmx.l.google.com
5   alt2.aspmx.l.google.com
10  alt3.aspmx.l.google.com
10  alt4.aspmx.l.google.com
```

You are **adding A records**, which is a different record type. MX and A coexist
fine. Nothing below asks you to remove, edit, or replace an MX record. If a form
ever offers to "replace existing records," say no.

### 2. Do not overwrite the SPF record

This TXT record exists today and is also email infrastructure:

```
TXT  @   v=spf1 include:_spf.google.com ~all
```

This matters because the Google Search Console verification in Step 5 is **also
a TXT record on `@`**. A domain can hold several TXT records at once, so the
correct move is **Add New Record**. If you instead edit the SPF row and paste the
verification string over it, your outbound mail starts failing SPF and landing in
spam. Two separate TXT rows, both on `@`. That is what correct looks like.

If mail ever does break: the two records above are the originals. Put them back.

---

## Step 1: Add the four A records

Namecheap → Domain List → wholeyield.com → **Manage** → **Advanced DNS** →
**Add New Record**, four times:

| Type     | Host | Value             | TTL       |
| -------- | ---- | ----------------- | --------- |
| A Record | `@`  | `185.199.108.153` | Automatic |
| A Record | `@`  | `185.199.109.153` | Automatic |
| A Record | `@`  | `185.199.110.153` | Automatic |
| A Record | `@`  | `185.199.111.153` | Automatic |

All four. They are GitHub's redundant Pages servers, not alternatives to pick
from. (Source: GitHub Pages apex-domain docs, checked 2026-07-15.)

## Step 2: Add www

| Type         | Host  | Value                       | TTL       |
| ------------ | ----- | --------------------------- | --------- |
| CNAME Record | `www` | `whole-yield.github.io.`    | Automatic |

This makes www.wholeyield.com redirect to the apex. Keep the trailing dot.

## Step 3: Delete any parking records

Namecheap ships domains with a default **URL Redirect Record** or a CNAME on `@`
or `www` pointing at `parkingpage.cash` or similar. If you see one, delete it.
It will fight the A records.

Delete only parking/redirect rows. Not the MX rows. Not the SPF TXT row.

## Step 4: Wait, then confirm

Give it 30 minutes or so. Then, from your Mac:

```bash
dig +short wholeyield.com A      # want the four 185.199.x.153 addresses
dig +short wholeyield.com MX     # want the five aspmx rows, unchanged
dig +short wholeyield.com TXT    # want the SPF row, still there
curl -sI https://wholeyield.com | head -1   # want HTTP/2 200
```

That second and third command are the email safety check. Run them.

## Step 5: Enforce HTTPS

Once the A records resolve, GitHub provisions a Let's Encrypt certificate. This
can take up to 24 hours and cannot be rushed.

Then: repo → **Settings** → **Pages** → tick **Enforce HTTPS**. The checkbox is
greyed out until the certificate is issued, which is normal. Come back later.

---

## Step 6 (start it today): Google Search Console

**This does not wait on any of the above.** DNS TXT verification proves you own
the domain whether or not a site answers on it. You can do it right now, in
parallel, while the A records propagate.

1. Go to <https://search.google.com/search-console>
2. **Add property** → the **Domain** option on the left (not "URL prefix")
3. Enter `wholeyield.com`
4. It hands you a TXT record that looks like `google-site-verification=...`
5. In Namecheap Advanced DNS: **Add New Record** → TXT Record → Host `@` → paste
   the value

**Add New Record. Do not edit the SPF row.** See the warning at the top. When
you are done there should be two TXT rows on `@`: the SPF one and the Google
one.

6. Back in Search Console, click **Verify**.

---

## What is already done

- Site built, `index.html` at the repo root
- `CNAME` committed with `wholeyield.com`
- GitHub Pages configured to serve `main` / root
- Repo public, which Pages requires for a custom domain to be publicly reachable

## What is left, in order

1. You: the DNS records above (Steps 1 to 3)
2. Wait for propagation, confirm with the `dig` checks (Step 4)
3. You: tick Enforce HTTPS once the cert lands (Step 5)
4. You: Search Console verification (can start immediately)
5. Then Play Console has a real URL to accept and verify
