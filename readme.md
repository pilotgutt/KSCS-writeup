# CYBERWEEK 2023 X KONGSBERG CSC<br>CTF WRITE-UP 23.09.2023 @ USN VESTFOLD

<i>Vi hadde en utrolig lærelik og givende opplevelse og stilte med laget vårt **$10^{-9}$**. Takk til **KCSC** og **VOLT** for et bra opplegg.</i><br><br>

## CATEGORY MISC:

warm_welcome
------------

<img width="800" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/ada72afb-b9ac-4ea4-ba7f-935cd9c3efd3">

<br>Her fulgte vi lenken som er gitt i oppgaveteksten.<br>
Vi brukte "inspiser element" for å lete etter flagget i kildekoden for nettsiden.<br><br>
Etter å ha letet litt, fant vi en kommentar i koden under "stillinger" - der fant vi flagget vårt.<br><br>

<img width="862" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/0d40f6c3-51f3-4f40-bdf4-8d5ea1d6157e">

<br><i>KCSC{922ec9531b1f94add983a8ce2ebdc97b}</i>

Speak Clearly
--------------
<img width="796" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/cb124bc9-73fe-41e2-a6ce-3f3fa6d9310e">

<br>Vi lastet først ned filen comms.txt som var vedlagt oppgaven og åpnet denne.<br><br>

<img width="852" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/99393073-3800-4641-b937-7c07c1e614e2">

<br>Her ser vi klart å tydelig at det er brukt det fonetiske alfabetet, og regner da med at det danner ord - som gir oss innholdet i flagget.<br>
Vi prøvde først å dekrypte den manuelt, men fant til slutt et verktøy som kunne konverte de fonetiske bokstavene om til vanlige bokstaver.<br>

Nettsiden vi brukte var: https://convertcase.net/nato-alphabet-translator/<br><br>

<img width="1198" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/7b356a81-fc35-4abd-9151-9c887281890e">

<br>Da fant vi ut at flagget skulle inneholde ordet "transmission".<br>

<i>KCSC{transmission}</i>

Password Manager
----------------
<img width="797" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/5c96b4a9-ffbf-4d98-bd6d-7e44e6459bfa">

<br>Her lastet vi ned secret.zip og pakket ut filen med 7Zip.<br>
Da fant vi filen secret.kdbx<br>
Vi startet med å bruke følgende kommando i Kali Linux:<br>
```linux
$ file secret.kdbx
```
<br>Da klarte vi å finne ut at filtypen var `Keepass password database 2.x KDBX`<br><br>
![image](https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/e1290d2a-a2b0-4340-940f-005b903b76ca)
<br>Her bruker vi keepass2john for å få ut hashen til filen i .txt format.

<br>Som det står i oppgaveteksten så er dette en databasefil som inneholder alle passordene lagret i en spesifik Keepass passord-database. 
<br>Vi brukte `John The Ripper` i Kali Linux for å brute-force oss til et passord som kunne brukes for å låse opp Keepass passordbanken.<br>
```linux
$ keepass2john secret.kdbx > keepasshash.txt
```
<br>I oppgaven så har dem hintet til at det kan være lurt å benytte en bra wordlist, spesifikt rockyou.txt - så vi benyttet denne.<br>
```linux
$ john --wordlist=rockyou.txt keepasshash.txt
```

<br>Vi lot John jobbe i et lite minutt, og kom tilbake med følgende svar:<br><br>

![image](https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/3e2da407-42c8-4ae2-9c5d-3a94d8e502a0)

<br><br>... og kommer tilbake med at `unpredictable` er passordet vi kan benytte for å låse opp passordbanken `secret.kdbx`<br>
Vi lastet ned `Keepass 2`, valgte `secret.kdbx` - og skrev inn passordet `unpredictable`:<br><br>
![image](https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/dd231124-b216-4de9-9915-b12f79b2df75)
<br><br>Her er brukernavnet flagget vi er ute etter, enkelt og greit!<br><br>

![image](https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/9144d986-d1fa-4842-9b42-a570eb01ae18)
<br><br><i>KCSC{P4ssword_manag3r_crack3r}</i><br>

Hugin
-----

<img width="795" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/1d791f99-93cb-4a0b-8e58-8448b4c5d436">

<br>Vi lastet ned dump.zip og unzippet med 7zip.<br>
Da fant vi filen `dump.txt`<br><br>

<img width="738" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/3157c100-3a34-475f-a969-c072d735c219">

<br><br>Her er det mange alfanumeriske verdier i et mønster - og vi tenkte at informasjonen kunne være `base64` encoded.<br>
Da prøvde vi å bruke `CyberChef` (https://gchq.github.io/CyberChef/) for å konverte til et leselig format:<br><br>

<img width="1098" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/e2a19a9a-3080-4a7c-a8fa-a524c28cdd96">

<br><br>Her ser vi at vi får ut en type kode med koordinat-informasjon.<br>
Etter et kjapt søk på nett, så finner vi ut at koden er et GeoJSON objekt.<br>
Vi ønsket å visualisere denne koden for å få det på et kart, siden oppgaven sier at flagget er på slutten av "pathen" tegnet på kartet.<br>
Vi fant et verktøy på nett som heter `geojson` (https://geojson.io/) og inputet koden:<br><br>

<img width="1371" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/4975ac0a-e807-4a27-a321-606557614825">
<br><br>
<img width="923" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/49037f20-235c-4a9d-8512-13298b331e77">
<br><br>

<i>KCSC{geojsoniscool}</i><br>

Weird Sound
-----------

<img width="798" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/dfbccb6b-ae7d-496e-80fd-84d673d83f66">

<br><br>Vi laster ned `whatsthatsound.zip` og unzipper slik at vi finner filen `whatsthatsound.wav`
<br>Når vi spilte av lydfilen, så var det bare vanlige VHF coms på radio og deretter noen rare lyder på slutten.
<br>Vi tenkte umiddelbart at det kunne være lurt å analysere lyden med programmet `Audacity`<br><br>

<img width="938" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/bfb6bffd-e861-4b50-a2dd-447d4466eb94">

<br><br>Vi testet med å se på lydfilen som Spektrogram.<br><br>

<img width="339" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/ebb28dd9-51a8-42d3-9c3c-30296e29fbb3">
<br><br>Vi fant da flagget på slutten av lydfilen og zoomet inn for å se det tydligere.<br><br>
<img width="857" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/fdb8aa4d-4f5f-49de-8bf4-09b5eeb6429e">

<br><br>KCSC{TONE_DEAF_TUNES}<br>

Discord Flaggsørviss
-------------------
<img width="795" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/ad762b55-8815-4aa0-a5aa-e09c670c1d10">


