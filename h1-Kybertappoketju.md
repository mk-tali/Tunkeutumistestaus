# h1 Kybertappoketju

## x) Lue/katso/kuuntele ja tiivistä.  
Herrasmieshakkerit  
-Vieraana Keskon tietoturvajohtaja Juho Rikala  
-Kesko on Suomen suurin konserni  
-Päivittäin mietitään mitä kautta Keskoa vastaan voidaan hyökätä  
-Isoin haaste palveluntarjoajien tietoturva  
-Täysin keskitetty tietoturva tiimi  
-Asiakkaista kerätään tietoa vain, jos asiakas on antanut luvan  
-Tiedot on kullekkin käyttötarkoitukseen suunnitellulla tietovarannolla  
(Herrasmieshakkerit 2024)  

Intrusion Kill Chain.  
-Hyökkäysketju on systemaattinen prosessi, jonka avulla saadaan haluttu vaikutus  
-Tietoverkkojen hyökkäysketjussa on seitsemän vaihetta: 1. Tiedustelu 2. Aseistaminen 3. Toimitus 4. Hyväksikäyttö 5. Asennus 6. Komento ja ohjaus 7. Tavotteiden toteuttaminen.  
(Hutchins et al. 2011.)  

Surveying Essential Tools for Active Reconnaissance: Port Scanning and Web Service Review  
-Nmap on suosituin porttiskanneri  
-Masscan on nopein porttiskanneri  
-Udpprotoscanner on nopea UDP porttiskanneri  
-Yksinkertaiset komennot joita saa muokattua eri parametreilla  
-EyeWitness priorisoi web sovelluksia ottamalla kuvakaappauksia  
(Santos 2019)  

KKO:2003:36  
-1998 A oli porttiskannannut osuuspankkikeskuksen portteja  
-A joutui korvaamaan osuuskunnalle 20 000-  ja yhtiölle 55 000 markkaa  
(Finlex. 2003.)  

## a) Asenna Kali virtuaalikoneeseen  
Minulla oli jo Kali asennettuna virtuaalikoneessa. Asensin Kali 2026.3 Virtualboxille.  

## b) Irrota Kali-virtuaalikone verkosta  
Asensin ohjeiden mukaan HacTheBox VPN:n. Sen avulla sain yhteyden pois verkkoon.  
<img width="537" height="183" alt="image" src="https://github.com/user-attachments/assets/cb655968-c4f2-4b1b-9f3a-bcbed64c0e02" />  
<img width="570" height="183" alt="image" src="https://github.com/user-attachments/assets/f31f3e35-77e5-4318-88bf-9c53da281d0c" />  
Ajoin komennon `nmap -T4 -A localhost`  
<img width="833" height="270" alt="image" src="https://github.com/user-attachments/assets/45c2bf3e-76fc-4e6d-9742-dad888a9d182" />  
-T4 Parametri kertoo kuinka nopeasti nmap skannaa, -A on agressiivinen skannaus, ottaa käyttöön käyttöjärjestelmän tunnistuksen, versiontunnistuksen, skriptiskannauksen ja reitityksen jäljityksen. Localhost skannaa vain localhost IP-osoitteen.  

## c) Porttiskannaus  

## d) Asenna kaksi vapaavalintaista demonia ja skannaa uudelleen. Analysoi ja selitä erot  

## e) HackTheBox  



## Lähteet  
Finlex. 2003. KKO:2003:36. https://www.finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36  
Herrasmieshakkerit. 25.9.2024. Tietoturvan Niksipirkka, vieraana Juho Rikala | 0x34. https://open.spotify.com/episode/4jBaSSkXdfsEWJrg0QRaVA?si=8693682c057c470b  
Hutchins et al. 2011. Intelligence-Driven Computer Network Defense
Informed by Analysis of Adversary Campaigns and
Intrusion Kill Chains. 3.2 Intrusion Kill Chain. https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf  
Santos et al. 2019. The Art of Hacking (Video Collection): 4.3 Surveying Essential Tools for Active Reconnaissance. https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_03/  

