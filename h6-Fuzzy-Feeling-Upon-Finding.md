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
Löysin GitHubista uusimman ffuf version 2.3.0, jonka tarvitsee näihin tehtäviin. Latasin sen komennoilla  
`wget https://github.com/ffuf/ffuf/releases/download/v2.3.0/ffuf_2.3.0_linux_amd64.tar.gz`  
`wget https://github.com/ffuf/ffuf/releases/download/v2.3.0/ffuf_2.3.0_checksums.txt`  
`sha256sum --ignore-missing -c ffuf_2.3.0_checksums.txt`  
`tar -xzf ffuf_2.3.0_linux_amd64.tar.gz`  
`sudo mv ffuf /usr/local/bin/ffuf`  
Tämän jälkeen `ffuf -V` näytti vielä versioksi 2.1.0, koska minulla oli myös se asennettuna koneella. Komennolla `which -a ffuf` näki kumpaa ffufia kone käyttää ja `sudo apt remove ffuf` sai poistettua vanhan ffufin.  
<img width="209" height="74" alt="image" src="https://github.com/user-attachments/assets/c9030a72-6610-4a76-a4a7-df7c3bd0e899" />  
Nyt on oikea versio asennettuna.  
(Joohoi 2026)  

## c1) Content discovery  
Katsoin tehtäväsivulta Getting started kohtaa ja ajoin siinä näkyvät komennot.  
`curl -O https://ffuf.io.fi/wordlists/content.txt`  
`curl -O https://ffuf.io.fi/wordlists/passwords.txt`  
Tämän jälkeen aloitin tehtävän kokeilemalla komentoa `ffuf -w content.txt -u https://ffuf.io.fi/FUZZ`, joka näkyi myös Getting started kohdassa.  
<img width="623" height="368" alt="image" src="https://github.com/user-attachments/assets/74871dc6-1564-4685-9f30-9dfa4d3457ec" />  
<img width="745" height="25" alt="image" src="https://github.com/user-attachments/assets/91687f6f-e448-4589-8b3a-f4ba21a11f2e" />  
Tässä komennossa ei oltu suodatettu mitään, joten se antoi valtavan määrän tuloksia. Tehtävänannossa näkyi flagit joita voi käyttää, ja muistinkin -ac eli autocalibration flagin tunnilta. Kokeilin ajaa komennon sen kanssa. Nyt tulostus oli huomattavsti lyhyempi ja siinä näkyi kaikki normaalista poikkeava.  
<img width="750" height="623" alt="image" src="https://github.com/user-attachments/assets/2fc3cd84-0391-4f01-904e-1f102ca447b7" />  
Kun luin seuraavia tehtäviä, oletin, että tämä oli oikea tulos.  

## c2) The interesting non-200  
Tässä tehtävässä tarkoituksena on löytää kaksi kiinnostavaa koodia, jotka ei ole 200. 
Kokeilin komentoa `ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -mc all -fc 200` Tässä -mc näyttää kaikki koodit, ei vain ffufin oletustuloksia ja -fc saadaan filtteröityä pois koodit, mitä ei haluta. Sain tulokseksi.  
<img width="744" height="518" alt="image" src="https://github.com/user-attachments/assets/bb8f2205-97ea-4a1a-81d1-4a8329a5e4e7" />  




## Lähteet  
Karvinen Tero. 2026. Tunkeutumistestaus. https://terokarvinen.com/tunkeutumistestaus/  
Hoikkala Joona. 2026. fuzzing with Ffuf. https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf  
Vault line. How to play. https://ffuf.io.fi/play  
Hoikkala Joona (Joohoi). 2026. ffuf. https://github.com/ffuf/ffuf  

