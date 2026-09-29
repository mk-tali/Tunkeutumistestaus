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
Tehtävänannossa lukee näin. "Two planted paths do not answer 200. One of them a default run will not even consider.", mutta molemmat, 301 ja 403 koodit näkyivät default ajossa. Oletan, että tarkoituksena oli löytää koodi 403 ja jokin toinen yksittäinen, mutta en sivun ohjeiden, enkä diaesityksen avulla keksinyt miten toisen saisi.  
(Hoikkala 2026) (Vault line)  
Jatkoin eteenpäin ja c4 tehtävän jälkeen palasin tähän.  
Kokeilin tehdä tätä tehtävää seclist sanakirjan avulla. Kysyin Claudelta, mitä sanalistoja kannattaa kokeilla ja se ehdotti seuraavia:  
`/usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt`  
`/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt`  
`/usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt`  
Ajoin komentoa `ffuf -w "sanakirja" -u https://ffuf.io.fi/FUZZ -mc all -fc 200,301,403`, mutta mikään näistä ei löytänyt toista koodia. Sanakirjat alkoivat mennä niin laajaksi ja niissä kesti niin kauan aikaa käydä läpi, ettei minulla ollut aikaa käydä jokaista läpi. Lopetin tehtävän tähän.  

## c3) Recursion  
Tässä tehtävässä on tarkoituksena mennä syvemmälle tuloksiin rekursion avulla. Rekursion avulla ffuf menee löydettyihin hakemistoihin ja fuzzaa uudelleen niiden sisällä. Kokeilin aluksi laittaa ohjeissa näkyvät flagit perus ffuf komennon perään. Aloitin `recursion-depth 2` ja katsoin mitä tulee. `ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -recursion -recursion-depth 2` ajoin tämän komennon ja huomasin, että tulostusta tuli niin suuri määrä, ettei sitä pysty käymään läpi niin lisäsin perään vielä -ac ja ajoin uudestaan.   
Ensimmäisenä tästä osui silmään seuraava kohta.  
<img width="834" height="180" alt="image" src="https://github.com/user-attachments/assets/64a44c5d-18d5-40b2-9c79-0f01eca4e958" />  
Ffuf löysi hakemiston, mutta recusrion-depth ei riittänyt. Asjoin seuraavaksi saman komennon ilman, että määrittelen syvyyttä, jolloin ffuf jatkaa niin syvälle kunnes kaikki on löydetty. `ffuf -w content.txt -u https://ffuf.io.fi/FUZZ -recursion -ac` Aikaisemman kohdan alta löytyi nyt vielä tämä kohta.  
<img width="940" height="200" alt="image" src="https://github.com/user-attachments/assets/b5955da0-b390-446a-bdae-e8ffb7fc4ef5" />  

## c4) Virtual hosts  
Tässä tehtävässä tarkoituksena on läytää kolme ffuf.io,fi alla olevaa hostia.  
Tässä fuzzataan host kohtaa, eikä URL:ia. Laitoin tehtävässä näkyvän -H flagin perus komennon perään. `ffuf -w content.txt -u https://ffuf.io.fi/ -H "Host: FUZZ.ffuf.io.fi"`  
<img width="725" height="765" alt="image" src="https://github.com/user-attachments/assets/66248f2a-8f64-4d1a-bb22-c7c857572b1b" />  
Tulosteesta tuli taas todella suuri, joten lisäsin -fw perään, jolla suodatin pois kaikki kohdat joissa oli 377 sanaa.  
<img width="751" height="468" alt="image" src="https://github.com/user-attachments/assets/0ecd3094-b80c-4423-b2f9-a67882802eb0" />  
Tällä komennolla löytyi yksi.  
Koska tässä ja c2 tehtävissä ei löytynyt tarpeeksi kohteita, ajattelin, että ehkä ongelmana on sanakirjat. Muistin tunnilla maininnan seclists sanakirjasta ja löysin sen diaesityksestäkin. Latasin itselleni sen ja kokeilin tätä tehtävää uudestaan sen avulla. Ajoin komennon `ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt  -u https://ffuf.io.fi -H "Host: FUZZ.ffuf.io.fi" -fw 377`  
Uudella sanakirjalla sain kaikki kolme näkyviin.  
<img width="938" height="499" alt="image" src="https://github.com/user-attachments/assets/9e033f9d-b160-4a82-8951-590646e74d86" />  




## Lähteet  
Karvinen Tero. 2026. Tunkeutumistestaus. https://terokarvinen.com/tunkeutumistestaus/  
Hoikkala Joona. 2026. fuzzing with Ffuf. https://terokarvinen.com/tunkeutumistestaus/hoikkala-2026-fuzzing-with-ffuf.pdf  
Vault line. How to play. https://ffuf.io.fi/play  
Hoikkala Joona (Joohoi). 2026. ffuf. https://github.com/ffuf/ffuf  

