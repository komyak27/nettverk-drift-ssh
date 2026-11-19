# Brukerstøtte-logg

Her er sakene jeg løste mens jeg satte opp og testet SSH-tilgangen. Jeg skrev dem som saker i en brukerstøtte, med spørsmål, årsak og løsning.

## Sak 1: Får ikke logget inn, «Permission denied»

| | |
|---|---|
| Dato / tid | 19.11.2026, kl. 18:37 |
| Bruker | Meg selv, fra mobilen (Termux) |
| Henvendelse | «Jeg skriver passordet, men får Permission denied tre ganger på rad.» |
| Spørsmål jeg stilte | Kom du fram til passord-spørsmålet? (Ja, så nettverk og brannmur er OK.) Hvilken bruker prøver du? (komya.) Hvordan logger du inn på PC-en til vanlig? (Med PIN.) Er kontoen en Microsoft-konto? (Ja.) |
| Feilsøking | Sjekket `Get-LocalUser` på PC-en. PrincipalSource var `MicrosoftAccount`. PIN-koden fungerer bare lokalt i Windows, ikke over SSH. |
| Årsak | SSH krever det ekte passordet til kontoen. Med Microsoft-konto og PIN vet ikke brukeren alltid dette passordet. |
| Løsning | Laget en lokal bruker `sshbruker` med eget passord. Logget inn med den. Fungerte med en gang. |
| Tid brukt | Ca. 10 minutter |
| Forebygging | Skrev i brukerveiledningen at brukernavnet er `sshbruker`, ikke den vanlige Windows-brukeren. |

## Sak 2: Brannmurregelen min hadde ingen effekt

| | |
|---|---|
| Dato / tid | 19.11.2026, kl. 18:25 |
| Bruker | Meg selv, som administrator på PC-en |
| Henvendelse | «Jeg laget en regel som bare slipper inn 192.168.0.0/24, men jeg er ikke sikker på om den faktisk begrenser noe.» |
| Spørsmål jeg stilte | Finnes det andre regler for port 22? Hvem laget dem? |
| Feilsøking | Kjørte `Get-NetFirewallRule -DisplayName "*OpenSSH*"`. Fant regelen «OpenSSH SSH Server (sshd)» som Windows laget automatisk. Den var aktiv og hadde ingen begrensning på adresse. |
| Årsak | Når to regler tillater samme port, vinner den åpne regelen. Min begrensede regel ble aldri brukt. Dette står også i kompendiet under «Regelkonflikter». |
| Løsning | `Set-NetFirewallRule -DisplayName "OpenSSH SSH Server (sshd)" -RemoteAddress 192.168.0.0/24`. Sjekket med `Get-NetFirewallAddressFilter`. Nå er begge reglene begrenset. |
| Tid brukt | Ca. 5 minutter |
| Forebygging | Sjekk alltid alle regler for en port, ikke bare den du laget selv. |

## Sak 3: Ping vises ikke i Wireshark

| | |
|---|---|
| Dato / tid | 19.11.2026, kl. 18:57 |
| Bruker | Meg selv |
| Henvendelse | «Jeg kjørte ping, og ping svarte, men i Wireshark med filteret `icmp` er det bare Port unreachable, ingen Echo request.» |
| Spørsmål jeg stilte | Hvor skrev du ping-kommandoen? Hva sto det i prompten? (Det sto `sshbruker@STAS`.) |
| Feilsøking | Prompten viste at jeg var inne i SSH-økten. Da kjørte ping på PC-en, og PC-en pinget sin egen adresse. Slik trafikk går ikke ut på Wi-Fi, så Wireshark ser den ikke. |
| Årsak | Feil sted å kjøre kommandoen. Ping må kjøres fra klienten (mobilen), ikke fra serveren. |
| Løsning | Skrev `exit` til jeg var tilbake i Termux (`~ $`). Kjørte `ping -c 4 192.168.0.207`. Wireshark viste da fire Echo request og fire Echo reply. |
| Tid brukt | Ca. 5 minutter |
| Forebygging | Se alltid på prompten før du kjører en kommando. Den forteller hvilken maskin du er på. |
