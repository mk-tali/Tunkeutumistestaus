# h4 Täysin Laillinen Sertifikaatti  
## x) Tiivistelmä  
## OWASP TOP 10:2021  
-94% sovelluksista testattu jonkinlaisella broken access controllilla.  
-Access control menetelmän idea on se, että käyttäjät eivät voi toimia omien oikeuksien ulkopuolella.  
-Toimii vain jos hyökkääjä ei pääse muokkaamaan metadataa tai access control checkejä.  
(OWASP TOP 10, 2021)  

## PortSwigger Academy
### Insecure direct object references (IDOR)  
-Access Control tyyppinen haavoittuvuus.  
-Hyökkääjä voi muokata URL:ia ja päästä näkemään salaisia tietoja.  
(PortSwigger IDOR)

### Path traversal  
-Tunnetaan myös nimellä Directory traversal.  
-Päästää hyökkääjän lukemaan sattumanvaraisia tiedostoja palvelimella jossa pyörii sovellus.  
-Muokkaamalla hakemisto polkua URL:issa hyökkääjä voi päästä salaittuihin tiedostoihin.  
-Tehokkain tapa ehkäistä path traversal liittyviä haavoittuvuuksia on välttää käyttäjän antaman syötteen välittämistä tiedostojärjestelmän rajapinnoille kokonaan.  
(PortSwigger Path traversal)  

### Cross-site scripting  
-Mahdollistaa hyökkääjän esiintyä uhrina, jolloin voi tehdä kaikkea mitä uhrikin.  
-Manipuloidaan nettisivua niin, että se palauttaa haitallista javascriptiä käyttäjälle.  
-Kolme tyyppiä: reflected, stored ja DOM-based.  
-Puolustatutuminen syötteiden suodatuksella, tulosteen oikealla enkoodauksella ja oikeat Content-Type headerit sekä Content Security Policyt.  
(PortSwigger Cross-site scripting)  

## a) Totally Legit Sertificate  
Aloitin ajamalla komennon `sudo apt-get install zaproxy`, joka löytyi kurssin tehtäväsivulta. (Karvinen 2026)  
<img width="698" height="444" alt="image" src="https://github.com/user-attachments/assets/709182aa-5338-4f6a-8972-84ff6ec79ca9" />  
Käynnistin zaproxyn komennolla `zaproxy`. Menin kohtaan Tools -> Options -> Network -> Server Certificates. Tässä näkyi generoituna sertifikaatti.  
<img width="1149" height="1077" alt="image" src="https://github.com/user-attachments/assets/96dfdbe9-324b-43e9-b53e-a3af3d98f859" />  
Tallensin sertifikaatin kotihakemistooni "Save" napista. Avasin Firefoxin ja hain Settings kohdasta "Certificate".  
<img width="665" height="234" alt="image" src="https://github.com/user-attachments/assets/abeaa818-c45a-40d7-ae8f-a49af126490e" />  
Sitten View Certificates, Authorities ja Import... Toin aikaisemmin tallentamani sertifikaatin ja valitsin seuraavan kohdan.  
<img width="798" height="303" alt="image" src="https://github.com/user-attachments/assets/d73c8714-2745-4c51-b2f5-71fb847b2c4b" />  
Seuraavaksi hain Firefoxin asetuksista "Proxy" ja avasin Network Settings asetukset. Laitoin asetukset seuraavanlaisesti.  
<img width="758" height="810" alt="image" src="https://github.com/user-attachments/assets/d0668253-31f2-4804-87d8-2d43e820489a" />  
Avasin PortSwigger sivun ja ZAP näytti tältä.  
<img width="1282" height="1321" alt="image" src="https://github.com/user-attachments/assets/d4182361-8395-43d3-9835-f84fb72076ec" />







## Lähteet  
OWASP TOP 10. 2021. Broken Access Control. https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/  
PortSwigger. Insecure direct object references (IDOR). https://portswigger.net/web-security/access-control/idor  
PortSwigger. Path traversal. https://portswigger.net/web-security/file-path-traversal 
PortSwigger. Cross-site scripting. https://portswigger.net/web-security/cross-site-scripting  
Karvinen, Tero. 2026. https://terokarvinen.com/tunkeutumistestaus/ 
