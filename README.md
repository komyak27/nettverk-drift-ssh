# Driftsprosjekt: Fjerntilgang til Windows-PC med SSH

**Fag:** Driftsstøtte og Brukerstøtte, Vg2 IT (2IMV)
**Av:** Stas
**Dato:** november 2026

Jeg satte opp sikker fjerntilgang til min egen PC (Windows 11 Home) med OpenSSH Server, konfigurerte brannmuren med PowerShell, koblet til fra mobilen og analyserte trafikken i Wireshark.

## Innhold

| Fil | Hva det er | Fag |
|---|---|---|
| [driftsdokumentasjon.md](driftsdokumentasjon.md) | Hvordan jeg satte opp og testet løsningen, steg for steg, med problemer og løsninger | Driftsstøtte |
| [brukerveiledning.md](brukerveiledning.md) | Veiledning for en bruker uten IT-bakgrunn: slik kobler du deg til | Brukerstøtte |
| [brukerstotte-logg.md](brukerstotte-logg.md) | Tre saker jeg løste underveis, skrevet som brukerstøtte-saker | Brukerstøtte |
| [skjermbilder/](skjermbilder/) | 29 skjermbilder fra hvert steg, nummerert | |

## Kort oppsummering

- OpenSSH Server installert og satt til automatisk start.
- Port 22 og ping (ICMP) åpnet i brannmuren, men bare for lokalnettet 192.168.0.0/24.
- Fant og fikset en automatisk brannmurregel som åpnet port 22 for alle.
- Egen lokal bruker `sshbruker` for fjerntilgang.
- Innlogging fra mobil (Termux) fungerer. Sett fra serveren: Established-forbindelse fra mobilen.
- Wireshark: SSH-trafikken er kryptert, ping vises som Echo request/reply, ARP viser IPv4-adressene i nettverket.

## Kilder

- Rasmussen, P. (2026). *Windows PowerShell, Konfigurere firewall, remote desktop og SSH*, v4-1.
- Rasmussen, P. (2026). *Wireshark, kun å vise IPv4-adresser*, v1.
- Microsoft Learn: OpenSSH for Windows.
- Cisco Networking Academy: Networking Basics.
