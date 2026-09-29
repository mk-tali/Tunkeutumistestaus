# h6 Fuzzy Feeling Upon Finding  

## Tiivistelmä  
### fuzzing with Ffuf  
-Tunkeutumistyökalujen swiss army-knife.  
-Käytetään sanalistoja, suodattimia ja avainsanoja.  
-Rajoita nopeutta.  
-Preflight ja postflight.  
(Hoikkala 2026)  

## a) Säännöt  
-Scope. Kohteena on sivusto ffuf.io.fi/play  
-Rules of engagement. Sivua saa fuzzata ffuf työkalulla.  
-Oikeudet tehdä tietoturvatestausta tähän kohteeseen perustuvat ylläpitäjän antamaan lupaan. Sivulla lukee, että siihen saa käyttää ffufia.  
-Riskit ja mitigointi. Riskinä on, että ffuf menee väärään kohteeseen, joka on rikos. Siksi on tärkeää tarkistaa ennen jokaista ajoa, että kohde on kirjoitettu täysin oikein.  
(Vault line)  

## b) Asenn ffuf versio, joka tukee aivan uutta preflight-ominaisuutta  
Löysin GitHubista uusimman ffuf version 2.3.0, jonka tarvitsee näihin tehtäviin. Latasin sen komennoilla `wget https://github.com/ffuf/ffuf/releases/download/v2.3.0/ffuf_2.3.0_linux_amd64.tar.gz` `wget https://github.com/ffuf/ffuf/releases/download/v2.3.0/ffuf_2.3.0_checksums.txt` 

## Lähteet  
Karvinen Tero. 2026. Tunkeutumistestaus. https://terokarvinen.com/tunkeutumistestaus/  
Hoikkala Joona. 2026. fuzzing with Ffuf. https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf  
Vault line. How to play. https://ffuf.io.fi/play
