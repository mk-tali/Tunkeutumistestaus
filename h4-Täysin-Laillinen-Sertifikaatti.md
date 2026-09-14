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



## Lähteet  
OWASP TOP 10. 2021. Broken Access Control. https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/  
PortSwigger. Insecure direct object references (IDOR). https://portswigger.net/web-security/access-control/idor  
PortSwigger. Path traversal. https://portswigger.net/web-security/file-path-traversal 
PortSwigger. Cross-site scripting. https://portswigger.net/web-security/cross-site-scripting  

