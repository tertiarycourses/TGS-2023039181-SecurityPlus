# Lab 17 — Site-to-Site VPN with WireGuard

You will build an encrypted tunnel between two simulated sites running in Linux network namespaces.

Run on https://killercoda.com/playgrounds/scenario/ubuntu

**Required software (free, apt):**
- `wireguard`, `wireguard-tools`
- `iproute2` (pre-installed)

---

## Step 1 — Install WireGuard

```bash
apt update && apt install -y wireguard wireguard-tools
modprobe wireguard
lsmod | grep wireguard
```

---

## Step 2 — Generate two key pairs

```bash
mkdir -p ~/wg && cd ~/wg
wg genkey | tee siteA.key | wg pubkey > siteA.pub
wg genkey | tee siteB.key | wg pubkey > siteB.pub
```

---

## Step 3 — Build two namespaces (Site A, Site B)

```bash
ip netns add siteA
ip netns add siteB
ip link add wgA type wireguard
ip link add wgB type wireguard
ip link set wgA netns siteA
ip link set wgB netns siteB
```

---

## Step 4 — Configure each tunnel endpoint

```bash
ip netns exec siteA wg set wgA private-key siteA.key listen-port 51820 \
   peer "$(cat siteB.pub)" allowed-ips 10.99.0.2/32
ip netns exec siteB wg set wgB private-key siteB.key listen-port 51821 \
   peer "$(cat siteA.pub)" allowed-ips 10.99.0.1/32

ip netns exec siteA ip addr add 10.99.0.1/24 dev wgA
ip netns exec siteB ip addr add 10.99.0.2/24 dev wgB
ip netns exec siteA ip link set wgA up
ip netns exec siteB ip link set wgB up
```

---

## Step 5 — Connect the tunnels via host loopback

```bash
ip netns exec siteA wg set wgA peer "$(cat siteB.pub)" endpoint 127.0.0.1:51821
ip netns exec siteB wg set wgB peer "$(cat siteA.pub)" endpoint 127.0.0.1:51820
```

---

## Step 6 — Verify

```bash
ip netns exec siteA ping -c3 10.99.0.2
ip netns exec siteA wg show
ip netns exec siteB wg show
```

`latest handshake` and incrementing `transfer` bytes prove the tunnel is up.

---

## Step 7 — Compare with IPsec / OpenVPN

| Property            | WireGuard | IPsec       | OpenVPN |
|---------------------|-----------|-------------|---------|
| Lines of kernel code| ~4 000    | ~400 000    | userspace |
| Crypto agility      | None — fixed suite | Negotiated | Negotiated |
| Roaming clients     | Built-in  | Add-on (MOBIKE) | Built-in |

WireGuard's small surface area is itself a security control.

---

## Free online tools

- **Tailscale (free tier, mesh on top of WireGuard)** — https://tailscale.com
- **NetMaker** — https://www.netmaker.io
- **OpenVPN Community** — https://openvpn.net/community/
- **strongSwan IPsec** — https://www.strongswan.org
- **WireGuard config generator** — https://www.wireguardconfig.com

---

## What you learned
- The four artefacts a WireGuard tunnel needs (priv key, peer pub key, endpoint, allowed-ips).
- Why "allowed-ips" doubles as routing **and** crypto-key routing.
- How a small protocol surface translates to a smaller attack surface.
