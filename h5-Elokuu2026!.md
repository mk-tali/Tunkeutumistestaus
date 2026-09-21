# h5 Elokuu2026!  
## x) Tiivistelmät  
### Cracking Passwords with Hashcat  
-Järjestelmät tallentaa salasanat hasheina, ei alkuperäisinä salasanoina.  
-Hasheja on eri tyyppejä, hashid tunnistaa tyypit.  
-Hashcat komentoon tulee `hashcat "hash tyyppi" "hash" "sanakirja"`  
(Karvinen 2022)  

### Crack File Password With John  
-Asennetaan tarvittavat ohjelmat.  
-Asennetaan ja konfiguroidaan John the Ripper, Jumbo.  
-Ensin extract hash uuteen tiedostoon .zip.hash  
-Sitten laitetaan john suorittamaan sanakirja hyökkäys hashiin.  
(Karvinen 2023)  

## a) Hashcat  
Minulla oli Kalilla jo hashcat, hashid ja wget asennettuna ja uusimmat versiot.  
<img width="916" height="296" alt="image" src="https://github.com/user-attachments/assets/ba50cf51-ce60-4228-8a14-09d5263508f4" />  
Latasin rockyou sanakirjan, että voin käyttää sitä tehtävissä. `wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz` `tar xf rockyou.txt.tar.gz` `rm rockyou.txt.tar.gz` (Karvinen 2022)  
<img width="291" height="63" alt="image" src="https://github.com/user-attachments/assets/34ce1762-36ee-461d-8f04-dd458757e3f9" />  
Tein komennolla `echo -n "password" |md5sum |tee example` harjoitussalasanalle "password" hashin ja tallensin sen example tiedostoon.  
<img width="378" height="65" alt="image" src="https://github.com/user-attachments/assets/8b1eae70-5098-49cf-aa32-66dab9140d06" />  
Tarkistin komennolla `hashid -m 5f4dcc3b5aa765d61d8327deb882cf99` hashin tyypin.  
<img width="384" height="108" alt="image" src="https://github.com/user-attachments/assets/ee5739c6-4fec-45f5-a82c-5c33c7b6b3da" />  
Sitten käytin hashcatia salasanan murtamiseen rockyou.txt tiedoston avulla. `hashcat -m 0 5f4dcc3b5aa765d61d8327deb882cf99 rockyou.txt` Hashcat tuotti paljon muutakin tulostetta, mutta kuvassa näkyy kohta, missä hashcat sai oikean salasanan.  
<img width="348" height="142" alt="image" src="https://github.com/user-attachments/assets/2b011b06-f5cf-4d23-8653-49cd09cd683f" />  

## c) John the Ripper  
Aloitin tarkistamalla, että minulla on kaikki tarvittavat työkalut tätä varten. Yritin ajaa komentoa `sudo apt-get -y install micro bash-completion git build-essential libssl-dev zlib1g zlib1g-dev zlib-gst libbz2-1.0 libbz2-dev atool zip wget` (Karvinen 2023), mutta sain virheen "E: Unable to locate package zlib-gst".  
<img width="941" height="126" alt="image" src="https://github.com/user-attachments/assets/062f4bfa-d79b-4227-9cbb-2d849dd7c664" />  
Ohjesivulla luki, että komennot ovat Debian 11:sta, niin kysyin Claudelta, onko Kalille jokin eri komento. Claude vastasi, että pakettia zlib-gst ei ole olemassa ja kyse on todennäköisesti kirjoitusvirheestä ohjesivun komennossa. Claude sanoi, että John the Ripperin pitäisi toimia ilmankin sitä. Ajoin komennon uudestaan ja jätin kohdan `zlib-gst` pois. Sain paketit asennettua ja jatkoin Johnin asennukseen.  
Kloonasin tarvittavan github sivun `git clone --depth=1 https://github.com/openwall/john.git`. Siirryin hakemistoon john/src/ ja ajoin komennon `./configure`.  
<img width="351" height="90" alt="image" src="https://github.com/user-attachments/assets/a927d15f-aa3b-40d7-a5b3-1039c0afcb4e" />  
<img width="658" height="466" alt="image" src="https://github.com/user-attachments/assets/64aefcb1-3dfa-47a9-b580-cf4486eacae4" />  
Tässä näkyvien kirjastojen pitäisi riittää tehtävän tekemiseen.  
Seuraavaksi ajoin komennon `make -s clean && make -sj4` ja parin minuutin jälkeen make prosessi oli valmis.  
Komennolla `ls -1` /john/run hakemistosta löytyi ajettavat ohjelmat ja skriptit.  
<img width="358" height="186" alt="image" src="https://github.com/user-attachments/assets/a4d9d825-d9ed-4b56-8796-5880fd309f2d" />  
Ajoin komennon `./john` ja näkyy, että John the Ripper on asennettu.  
<img width="934" height="97" alt="image" src="https://github.com/user-attachments/assets/768cd2fa-c0f6-428c-8ef6-6c15c8bc4469" />  
Poistin aikaisemmin luomasta example tiedostosta "-" hashin perästä, koska John the Ripper ei osaa käsitellä sitä. `cut -d' ' -f1 example > example.hash` Nyt tiedosto näyttää tältä.  
<img width="356" height="119" alt="image" src="https://github.com/user-attachments/assets/0f020d17-e941-4e1b-a503-decd199af1ee" />  
Siirryin /john/run ja ajoin komennon `./john --format=raw-md5 ~/h5-Elokuu2026\!/example.hash`. Tässä piti spesifioida hashin format, jotta John osaa käsitellä sen oikein.  
<img width="741" height="253" alt="image" src="https://github.com/user-attachments/assets/c288c810-b12a-4056-8f3a-f5fd5b55e80d" />  
Oikea salasana "password" löytyi.  

## e) Tiedosto  
Latasin aluksi ohjesivulta löytyvän zip tiedoston. `wget https://TeroKarvinen.com/2023/crack-file-password-with-john/tero.zip` (Karvinen 2023). Yritin unzipata sen, mutta vaati salasanan.  
<img width="895" height="368" alt="image" src="https://github.com/user-attachments/assets/f99648f3-3d2d-42a1-ba34-bb5af111507a" />  
Muutin tero.zip tiedoston tero.zip.hash tiedostoksi. `/john/run/zip2john tero.zip > tero.zip.hash`.  
<img width="946" height="230" alt="image" src="https://github.com/user-attachments/assets/cbaea3e1-3447-4e0f-bbd4-a1ace7737b12" />  
Ajoin komennon `./john ../../tero.zip.hash`, jolla John murtaa hashin. Sain salasanaksi "butterfly"  
<img width="798" height="269" alt="image" src="https://github.com/user-attachments/assets/50558e7b-cea4-41a2-a8ed-0a8beb6de488" />  
Menin unzippaamaan tero.zip tiedoston ja annoin salasanaksi "butterfly". Salasana oli oikein.  
<img width="367" height="96" alt="image" src="https://github.com/user-attachments/assets/a79413e9-3e93-4629-b82a-ced0055ed363" />  

## f) Tiiviste  
Loin käyttäjän "JtR".  
<img width="357" height="69" alt="image" src="https://github.com/user-attachments/assets/cd36a7fd-57b4-4198-87e2-1ad968bd5e0c" />  
Asetin salasanaksi "testi".  
<img width="367" height="101" alt="image" src="https://github.com/user-attachments/assets/1bb79386-ae2c-4df9-91ac-489941f59c42" />  
Ajoin komennon `sudo unshadow /etc/passwd /etc/shadow > ~/h5-Elokuu2026\!/JtR.hash`. Tämä yhdistää passwd:stä löytyvät käyttäjätunnukset shadow:sta löytyviin salasana hasheihin, että John the Ripper osaa yhdistää molemmista löytyvät tiedot käyttäjän salasanan murtamiseen.  
<img width="868" height="65" alt="image" src="https://github.com/user-attachments/assets/5aebfac8-f8c8-4cdf-8bee-fd2bdabfb579" />  
Ajoin komennon `./john ~/h5-Elokuu2026\!/JtR.hash`, mutta olibn väärässä hakemistossa. Siirryin oikeaan hakemistoon ja ajoin komennon uudelleen.  
<img width="367" height="193" alt="image" src="https://github.com/user-attachments/assets/91beaaf8-ff54-4f48-a28d-55830b94ddda" />  
Tässä tuli virheeksi "No password hashes loaded (see FAQ)" Googlasin tuon ja löysin openwallin FAQ sivun, jossa oli sama kysymys kuin minulla. Tämän sivun ja Clauden avulla selvisi, että ongelmana on ilmeisesti hash tyyppi. `./configure` tulosteessa näkyi kohta "Generic crypt(3) format - no" ja John the Ripper tarvitsee sen, että pystyy käsittelemään Kalin käyttäjien salasanoja, jotka tallennetaan yescrypt hashina. (Openwall) Yritin lisätä Generic crypt(3) formatin seuraavien vaiheiden avulla. Asensin libcrypt-dev kirjaston `sudo apt-get install -y libcrypt-dev`. /john/src hakemistossa `make -s clean`. `./configure`. Generic crypt(3) format oli silti ... no.  
<img width="655" height="235" alt="image" src="https://github.com/user-attachments/assets/8c2dc68b-d9d5-4797-9896-6a0d2c839cc7" />  
Ajoin `make -sj4` komennon ja siirryin seuraavaan vaihtoehtoon.  
Koska en saanut tuota lisättyä, päädyin muuttamaan JtR käyttäjän salasanan hashin SHA-512-crypt muotoon.  
<img width="771" height="71" alt="image" src="https://github.com/user-attachments/assets/d3a88b62-c046-4668-85ea-51e1ae55c066" />  
<img width="954" height="186" alt="image" src="https://github.com/user-attachments/assets/8e6505c5-8c4f-4669-8581-6d5dbd8bf9e6" />  
Kuvissa näkyy vaiheet miten muutin hashin `openssl` komennolla, vaihdoin sen JtR käyttäjälle `usermod` komennolla ja tallensin sen `unshadow` komennolla JtR.hash tiedostoon.  
Ajoin komennon `./john ~/h5-Elokuu2026\!/JtR.hash` ja nyt John the Ripper toimi kuten pitää. Oikea salasana käyttäjälle JtR löytyi.  
<img width="767" height="298" alt="image" src="https://github.com/user-attachments/assets/33e075c4-6784-45ea-b4ba-f10c84931386" />

## g) Sanakirja  
Tein oman sanakirjan hashcatille. Loin nanolla tiedoston mihin laitoin esimerkki salasanoja.  
<img width="301" height="55" alt="image" src="https://github.com/user-attachments/assets/43dd51a6-31c6-41ff-8f3b-de94f952ca32" />  
<img width="265" height="230" alt="image" src="https://github.com/user-attachments/assets/e25eed93-ebc6-4580-9690-cb10aab07c68" />  
Tarkistin, että tälläkin saa murrettua aikaisemmin luomani hashin.  
<img width="945" height="373" alt="image" src="https://github.com/user-attachments/assets/803ad90f-e8dd-4426-988b-6c39ebf930d5" />  

## h) Hash rules  
Loin uuden salasanan jota ei ole luomassani sanakirjassa.  
<img width="308" height="65" alt="image" src="https://github.com/user-attachments/assets/aa61a0c5-ec7e-430a-971c-71b2300976e3" />  
Löysin hashcat säännöt täältä.  
<img width="846" height="206" alt="image" src="https://github.com/user-attachments/assets/8421ffb0-6068-4d59-a6f1-46cc748843b4" />  
Kokeilin ilman sääntöjä ja ei löytynyt salasanaa. --potfile-disable estää hashcatia muistamasta aiemmin murrettuja salasanoja, joten vaikka salasana on murrettu, sen pitäisi näkyä tässä.  
<img width="667" height="69" alt="image" src="https://github.com/user-attachments/assets/9e16e6bf-4948-4171-93a3-987ebf2d890b" />  
<img width="603" height="352" alt="image" src="https://github.com/user-attachments/assets/41b5d21d-891f-4277-94b0-ae72f5902218" />  
Kokeilin seuraavaksi best66.rule kanssa, mutta sekään ei toiminut.  
<img width="949" height="229" alt="image" src="https://github.com/user-attachments/assets/ca7adcc1-0817-49b0-8550-4e3cc83fad10" />  
<img width="609" height="371" alt="image" src="https://github.com/user-attachments/assets/d5ab5a7c-b593-4aba-8658-276ded7b1376" />  
Claude sanoi tähän, että olisi parempi kokeilla salasanalla jossa on vain yksi muuttuja, kuten "Password". Loin tuolle salasanalle uuden hashin ja kokeilin murtaa sen.    
<img width="678" height="123" alt="image" src="https://github.com/user-attachments/assets/02533587-82a2-44f7-9da9-308aecf11983" />  
<img width="607" height="345" alt="image" src="https://github.com/user-attachments/assets/22def7d7-a3ee-4c3b-a975-941ac2d28aea" />  
Ilman sääntöjä ei onnistunut, kuten ei pitäisikään. Sitten säännön kanssa.  
<img width="944" height="83" alt="image" src="https://github.com/user-attachments/assets/582fd72d-ae97-4760-9cb0-32ea631bc5a6" />  
<img width="630" height="431" alt="image" src="https://github.com/user-attachments/assets/0d451e9a-5804-41c3-a092-0aabe1538fcd" />  
Nyt onnistui. Sääntö muutti sanakirjan sanan "password" muotoon "Password" ja löysi osuman hashiin. 


## Lähteet  
Karvinen Tero. 2022. Cracking Passwords with Hashcat. https://terokarvinen.com/2022/cracking-passwords-with-hashcat/  
Karvinen Tero. 2023. Crack File Password With John. https://terokarvinen.com/2023/crack-file-password-with-john/  
Openwall. John the Ripper FAQ. https://www.openwall.com/john/doc/FAQ.shtml  
