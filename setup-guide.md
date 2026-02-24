# OpenClaw on DigitalOcean

## 1. Create a Droplet
- Choose `Ubuntu 24.04 LTS`.
- Pick a region nearest to you (for example: `sg`).
- Select `Premium Intel`.
- Recommended size: `2 GB RAM / 1 Intel CPU / 70 GB NVMe`.

## 2. Generate and Add an SSH Key
If you do not already have an SSH key:

```bash
ssh-keygen -t ed25519 -a 100 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub
```

Add the public key to your Droplet in DigitalOcean.

## 3. SSH into the Server
```bash
ssh root@YOUR_IP
```

## 4. Create a Sudo User
```bash
sudo adduser --disabled-password --gecos "" clawuser && sudo usermod -aG sudo clawuser && echo 'clawuser ALL=(ALL) NOPASSWD: ALL' | sudo tee /etc/sudoers.d/clawuser >/dev/null && sudo chmod 440 /etc/sudoers.d/clawuser && su - clawuser
```

## 5. Add SSH Key for `clawuser`
Add your public key to:

- `~/.ssh/authorized_keys`

```bash
mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDER+t+pCERmQtr1z/nM5CRPZKeEF66oyF/MGdFpqC6jCUTX8DV31+OEeU7Pn76ulP4mu0Ey0P+0D3QVgiD7AB9BxVbfcH2cRbSt3zPebQtZ9nHT0+sp3kDz6jVi/rbsj2KwpEmFO/iPm+lIQ70sbx2Kz27qLlNv1NZJLrgid3VdNa+SDRU2OXUsGtDgxgxv1NwqBpKU7vq0T0rOpp1AOC2n1CllLgAckrsp7Hp1YU00xo1Xjdk0ZcaJC08FPPGoeSwgqLt+X+jEQeEVyhXMhQl6g4SI0nYfDh0Nh2pHFGzayxZnAoE3h+i+XQiTt9YDkkeqIUGQYyCmm6l0c7YQTtL universe@sets-mbp.lan" >> ~/.ssh/authorized_keys
```

Then log out and log back in as `clawuser`.

## 6. Install OpenClaw
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

You will need to install gateway if you 

```bash
openclaw gateway install
```

## 7. Start Gateway
```bash
openclaw gateway --port 18789 --verbose
```

## 8. Create SSH Tunnel to Access UI
```bash
ssh -L 18789:127.0.0.1:18789 clawuser@YOUR_IP
```

Open:
- http://127.0.0.1:18789

## 9. Open Dashboard
If you are trying to connect and cannot find the token, run:

```bash
openclaw dashboard
```

## 10. Troubleshooting
Run:

```bash
openclaw doctor
```

This diagnoses issues and surfaces risky or misconfigured settings.
