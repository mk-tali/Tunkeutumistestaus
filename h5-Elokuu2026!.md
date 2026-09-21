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




## Lähteet  
Karvinen Tero. 2022. Cracking Passwords with Hashcat. https://terokarvinen.com/2022/cracking-passwords-with-hashcat/  
Karvinen Tero. 2023. Crack File Password With John. https://terokarvinen.com/2023/crack-file-password-with-john/  
