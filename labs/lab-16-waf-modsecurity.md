# Lab 16 — Web Application Firewall (WAF) with ModSecurity

You will deploy nginx + ModSecurity 3 + the OWASP Core Rule Set, then watch it block real attack payloads.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `nginx`
- `libmodsecurity3`, `libnginx-mod-http-modsecurity`
- `modsecurity-crs`

---

## Step 1 — Install

```bash
apt update && apt install -y nginx libnginx-mod-http-modsecurity modsecurity-crs
```

---

## Step 2 — Enable ModSecurity in nginx

```bash
cat > /etc/nginx/modsec.conf <<'EOF'
Include /etc/modsecurity/modsecurity.conf
Include /usr/share/modsecurity-crs/owasp-crs.load
EOF

cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

cat > /etc/nginx/sites-available/default <<'EOF'
server {
  listen 80 default_server;
  modsecurity on;
  modsecurity_rules_file /etc/nginx/modsec.conf;
  root /var/www/html;
}
EOF

systemctl restart nginx
```

---

## Step 3 — Confirm CRS is loaded

```bash
nginx -T 2>/dev/null | grep -ci "SecRule"
```

You should see hundreds of loaded rules.

---

## Step 4 — Fire common attack payloads

```bash
curl -s -o /dev/null -w "%{http_code}\n" "http://127.0.0.1/?id=1' OR '1'='1"
curl -s -o /dev/null -w "%{http_code}\n" "http://127.0.0.1/?q=<script>alert(1)</script>"
curl -s -o /dev/null -w "%{http_code}\n" "http://127.0.0.1/?file=../../etc/passwd"
curl -s -o /dev/null -w "%{http_code}\n" "http://127.0.0.1/?cmd=;id"
```

Expect `403` for each — CRS recognises SQLi, XSS, path traversal, and command injection.

---

## Step 5 — Read the audit log

```bash
tail -50 /var/log/modsec_audit.log
grep -E "Matched|attack" /var/log/modsec_audit.log | tail
```

Each event records the rule ID, severity, and the offending payload.

---

## Step 6 — Tune a false positive

If a legitimate request is blocked, exempt the specific rule for that path:

```bash
echo 'SecRule REQUEST_URI "@beginsWith /admin/edit" "id:1000,phase:1,pass,nolog,ctl:ruleRemoveById=941100"' \
  >> /etc/modsecurity/modsecurity.conf
systemctl reload nginx
```

---

## Free online tools

- **OWASP CRS docs** — https://coreruleset.org
- **ModSecurity reference** — https://github.com/SpiderLabs/ModSecurity/wiki
- **Cloudflare WAF (free tier)** — https://www.cloudflare.com
- **AWS WAF managed rules (pay-as-you-go)** — https://aws.amazon.com/waf/
- **Wafw00f** — WAF detection: https://github.com/EnableSecurity/wafw00f

---

## What you learned
- A WAF is layer-7 inspection on top of an HTTP server.
- The OWASP CRS gives instant coverage of OWASP Top 10 with no custom rules.
- How to triage rule blocks and selectively turn off rules per path.
