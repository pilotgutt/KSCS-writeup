# CYBERWEEK 2023 X KONGSBERG CSC<br>CTF WRITE-UP 23.09.2023 @ USN VESTFOLD

<i>Vi hadde en utrolig lærelik og givende opplevelse og stilte med laget vårt **$10^{-9}$**. Takk til **KCSC** og **VOLT** for et bra opplegg.</i>

## CATEGORY MISC:

warm_welcome
------------

<img width="800" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/ada72afb-b9ac-4ea4-ba7f-935cd9c3efd3">

Her fulgte vi lenken som er gitt i oppgaveteksten.
Vi brukte "inspiser element" for å lete etter flagget i kildekoden for nettsiden.
Etter å ha letet litt, fant vi en kommentar i koden under "stillinger" - der fant vi flagget vårt.

<img width="862" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/0d40f6c3-51f3-4f40-bdf4-8d5ea1d6157e">

<i>KCSC{922ec9531b1f94add983a8ce2ebdc97b}</i>

Speak Clearly
--------------
<img width="796" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/cb124bc9-73fe-41e2-a6ce-3f3fa6d9310e">

Vi lastet først ned filen comms.txt som var vedlagt oppgaven og åpnet denne.

<img width="852" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/99393073-3800-4641-b937-7c07c1e614e2">

Her ser vi klart å tydelig at det er brukt det fonetiske alfabetet, og regner da med at det danner ord - som gir oss innholdet i flagget.
Vi prøvde først å dekrypte den manuelt, men fant til slutt et verktøy som kunne konverte de fonetiske bokstavene om til vanlige bokstaver.

Nettsiden vi brukte var: https://convertcase.net/nato-alphabet-translator/

<img width="1198" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/7b356a81-fc35-4abd-9151-9c887281890e">

Da fant vi ut at flagget skulle inneholde ordet "transmission".

<i>KCSC{transmission}</i>

Password Manager
----------------
<img width="797" alt="image" src="https://github.com/pilotgutt/KSCS2023CTF-writeup/assets/142602928/5c96b4a9-ffbf-4d98-bd6d-7e44e6459bfa">



