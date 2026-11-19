# Brukerveiledning: Slik kobler du deg til PC-en med SSH fra mobilen

**For:** Noen i familien eller en venn som skal bruke PC-en min hjemmefra, uten IT-bakgrunn
**Skrevet av:** Stas, 19.11.2026

## Hva er dette?

SSH er en måte å styre PC-en på fra en annen enhet, for eksempel mobilen. Du ser ikke skjermen til PC-en. I stedet skriver du kommandoer med tekst, og PC-en svarer med tekst. Alt som sendes er kryptert, så ingen andre kan lese det.

## Dette trenger du

- En Android-mobil som er koblet til **samme Wi-Fi** som PC-en. Mobildata fungerer ikke.
- Appen **Termux** (gratis, fra F-Droid eller Google Play).
- Brukernavn: `sshbruker`
- Passord: spør meg, jeg gir det muntlig. Ikke send det på melding.
- Adressen til PC-en: `192.168.0.207`
- PC-en må være på.

## Steg for steg

**1. Installer SSH i Termux (bare første gang).**
Åpne Termux og skriv:
```
pkg install openssh
```
Trykk Enter. Når den spør `[Y/n]`, skriv `y` og trykk Enter. Vent til den er ferdig.

**2. Koble til PC-en.**
Skriv:
```
ssh sshbruker@192.168.0.207
```
Trykk Enter.

**3. Svar «yes» første gang.**
Første gang får du et langt spørsmål som slutter med `(yes/no)?`. Dette er normalt. Mobilen spør om den kan stole på PC-en. Skriv `yes` og trykk Enter. Du får ikke dette spørsmålet neste gang.

**4. Skriv passordet.**
Du ser ingen tegn mens du skriver. Ikke stjerner heller. Det er normalt. Skriv passordet og trykk Enter.

**5. Nå er du inne.**
Du ser denne linjen:
```
sshbruker@STAS C:\Users\sshbruker>
```
Det betyr at alt du skriver nå, kjøres på PC-en. Prøv å skrive `hostname` og trykk Enter. Svaret skal være `Stas`.

**6. Avslutt.**
Skriv `exit` og trykk Enter. Du ser «Connection to 192.168.0.207 closed». Da er du ute.

## Vanlige problemer

| Det som skjer | Prøv dette |
|---|---|
| `Connection timed out` eller det bare står stille | Sjekk at mobilen er på samme Wi-Fi som PC-en. Sjekk at PC-en er på. Sjekk at du skrev adressen riktig: 192.168.0.207 |
| `Connection refused` | PC-en er på, men SSH kjører ikke. Si fra til meg, så starter jeg tjenesten |
| `Permission denied, please try again` | Feil passord eller feil brukernavn. Brukernavnet er `sshbruker` med små bokstaver. Prøv passordet en gang til, sakte |
| `The program ssh is not installed` | Du hoppet over steg 1. Skriv `pkg install openssh` |
| Teksten på skjermen er veldig liten | Dra to fingre fra hverandre på skjermen i Termux, da blir teksten større |

## Trenger du hjelp?

Send meg en melding med:
- et skjermbilde av feilen,
- hvilket steg du var på,
- om mobilen er på Wi-Fi hjemme.

Da er det mye lettere for meg å finne feilen.
