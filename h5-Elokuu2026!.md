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
Menin unzippaamaan ter.zip tiedoston ja annoin salasanaksi "butterfly". Salasana oli oikein.  
<img width="367" height="96" alt="image" src="https://github.com/user-attachments/assets/a79413e9-3e93-4629-b82a-ced0055ed363" />  

## f) Tiiviste  
Loin käyttäjän "JtR".
<img width="357" height="69" alt="image" src="https://github.com/user-attachments/assets/cd36a7fd-57b4-4198-87e2-1ad968bd5e0c" />  
Asetin salasanaksi "testi".  
<img width="367" height="101" alt="image" src="https://github.com/user-attachments/assets/1bb79386-ae2c-4df9-91ac-489941f59c42" />  



## Lähteet  
Karvinen Tero. 2022. Cracking Passwords with Hashcat. https://terokarvinen.com/2022/cracking-passwords-with-hashcat/  
Karvinen Tero. 2023. Crack File Password With John. https://terokarvinen.com/2023/crack-file-password-with-john/  
