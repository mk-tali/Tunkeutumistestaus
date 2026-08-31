# h2 DORA the Explora  
## x) Tiivistelmät  
DORA and TLPT testing  
-DORA = Digital Operations Resilience Act. EU:n laajuinen sääntely rahoitusalan häiriönsietokyvyn varmistamiseksi.  
-Viisi pilaria.  
-Vaatimukset kahteen testaustapaan.  
-TIBER-EU = Threat Intelligence-Based Ethical Red Teaming.  
-Testausprosessissa neljä vaihetta.  
-Pankkiautomaatteihin hyökätty.  
-Red teamin hyökkäyspolku, in - through - out.  
(Buuri 2026)  

DORA  
-Kun ICT testausta ei ole vaadittu, haavoittuvuudet jäävät huomaamatta.  
-Ilman unionin puuttumista asiaan, testaus jäisi epäjohdonmukaiseksi.  
-ICT-palvelut ovat alentaneet rahoituksen välityksen kustannuksia.  
(European Union 2022)  

TIBER-FI Testing phase.  
-Kaksi erillistä prosessin osaa.  
-Erilasia testaus metodeja.  
-Luodaan realistisia skenaarioita.  
(Suomen pankki 2025)  

## a)Metasploitable
Asensin Metasploitable 2 Virtualboxille Rapid 7 sivulta. 

## b) Virtuaaliverkko Kalin ja Metasploitable välillä  
Kali saa yhteyden verkkoon, ja yhteyden saa pois päältä.  
<img width="525" height="210" alt="image" src="https://github.com/user-attachments/assets/b354ee95-e733-40cc-ba11-a66a5e78516b" />  
Asetin molemmille koneille ipv4 osoitteet samasta aliverkosta.  
Tässä Kali.  
<img width="387" height="43" alt="image" src="https://github.com/user-attachments/assets/1cb23a64-9455-4a78-af56-63fe0a83043d" />  
<img width="805" height="259" alt="image" src="https://github.com/user-attachments/assets/bb0b2754-0f45-42e2-ba1f-d96d79ace2e9" />  
Tässä Metasploite.  
<img width="726" height="361" alt="image" src="https://github.com/user-attachments/assets/50c0df9f-ac74-4ca0-a089-f20906935114" />  
Kali saa yhteyden internettiin.  
<img width="517" height="193" alt="image" src="https://github.com/user-attachments/assets/931a6e4a-4019-4fa2-b5ff-8255f00c6671" />  

## c) Oma virtuaaliverkko  
Kali ei saa yhteyttä internettiin, mutta saa yhteyden Metasploitableen.  
<img width="556" height="289" alt="image" src="https://github.com/user-attachments/assets/ec129e4a-6c35-4982-abc1-9d2d31357593" />  
Metasploitable saa yhteyden Kaliin, mutta ei internettiin.  
<img width="590" height="228" alt="image" src="https://github.com/user-attachments/assets/be74c930-bc6d-4ce5-b3d7-d890eef1b97f" />  

## d) Porttiskannataan Metasploitable  
Nmap löysi Metasploitablen.  
<img width="561" height="172" alt="image" src="https://github.com/user-attachments/assets/f3ebdab8-c7de-4cd2-af25-331deeb6ef63" />  
<img width="600" height="493" alt="image" src="https://github.com/user-attachments/assets/8d6a3abd-c5aa-4ac7-be51-063e0831468b" />  

## e) Huolellinen porttiskannaus  
Ajoin komennon `sudo nmap -A -T4 -p- 192.168.56.20` ja nmap antoi todella kattavan tuloksen. Kysyin Claude.ai:lta mitkä portit olisivat parhaimmat analyysiin ja löysin niistä Rapid7 sivuilta tietoa. Valitsin seuraavat portit.  
21/tcp vsftpd 2.3.4.  
<img width="451" height="243" alt="image" src="https://github.com/user-attachments/assets/ca4c2ebb-75d6-4c72-af95-91e74cedf322" />  
CVE-2011-2523. Vuonna 2011 hyökkääjä sai asennettua tähän takaoven. Tätä kautta sai täyden pääsyn koneeseen ilman salasanaa. (Rapid7. VSFTPD 2.3.4 Backdoor Command Execution)  

3306/tcp MySQL 5.0.51a-3ubuntu5.  
<img width="922" height="163" alt="image" src="https://github.com/user-attachments/assets/5deab3e9-b686-4a4f-a239-3376c6b4664d" />  
Oletettiin, että MySQL käyttäessä `memcmp()` funktiota vertaamaan annettua salasanaa oikeaan, se palauttaisi aina arvon välillä -128 - 127. Tietyillä alustoilla funktio saattoi palauttaa alueen ulkopuolisen arvon, jolloin väärä salasana hyväksyttiin oikeana. (Rapid7. CVE-2012-2122: A Tragically Comedic Security Flaw in MySQL)  

## Lähteet  
Buuri. 2026. DORA and TLPT testing. https://terokarvinen.com/buuri-2026-dora-and-threat-lead-penetration-testing/buuri-2026-dora-and-threat-lead-penetration-testing--teros-pentest-course.pdf  
European Union. 2022. Regulation on digital operational resilience for the financial sector. Articles 26, 27. https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng  
Suomen pankki. 2025. TIBER-FI Procedures and Guidelines. 5.4 Testing phase. https://www.suomenpankki.fi/globalassets/bof/en/money-and-payments/the-bank-of-finland-as-catalyst-payments-council/tiber-fi/tiber-fi-2.0-procedures-and-guidelines.pdf  
Rapid7. VSFTPD 2.3.4 Backdoor Command Execution. https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/  
Rapid7. CVE-2012-2122: A Tragically Comedic Security Flaw in MySQL. https://www.rapid7.com/blog/post/2012/06/11/cve-2012-2122-a-tragically-comedic-security-flaw-in-mysql/  

