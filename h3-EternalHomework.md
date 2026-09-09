# h3 EternalHomework
## x) Lue ja tiivistä  
Mastering Metasploit  
-Perustermit: Exploits, Payload, Auxiliary, Encoders, Meterpreter.  
-Useita hyötyjä.  
-Tulokset kannattaa aina tallentaa.  
-`db_nmap` komennolla porttiskannaus.  
-Voi etsiä tiettyjä haavoittuvuuksia search komennolla.  
-Meterpreter sessiolla hyökkäys.  
-Tässä kappaleessa oli tunkeutumistestauksen vaiheet ja Metasploit perusteet.  
(JaswaL 2020)  

Mitä 'nmap -sn' tekee?  
-sn optio kertoo nmapille, että ei tee porttiskannausta host discoveryn jälkeen. Tämä tulostaa vain ne hostit, jotka vastasivat discovery probeihin. Tällä ei herätetä niin paljoa huomiota porttiskannatessa.  
(nmap.org)  
Uskon, että käyttämäni lähde on luotettava, koska se on nmapin virallinen sivusto.  

## b) Porttiskannauksen tulokset Metasploitin tietokantoihin  
Avasin Metasploitablen ja Kalin. Kalissa ajoin komennot `sudo msfdb init` ja `sudo msfconsole` Näin pääsin msf consoleen Kalilla. Metasploitablessa ajoin komennon `sudo ifconfig eth0 192.168.56.11 netmask 255.255.255.0 up`, koska sillä ei ollut ip osoitetta. Tämä on samassa aliverkossa Kalin kanssa. Nyt ping testit toimivat molempiin suuntiin.  
<img width="574" height="163" alt="image" src="https://github.com/user-attachments/assets/5a81871e-9677-40e6-ae8b-1ab65b2c666d" />  
<img width="545" height="242" alt="image" src="https://github.com/user-attachments/assets/a71662a0-a130-4570-9dd3-a5a4d4399a5d" />  
Ajoin komennon `db_nmap -sV 192.168.56.11` db_ tallentaa skannauksen tietokantaan.
<img width="1226" height="660" alt="image" src="https://github.com/user-attachments/assets/ac8d9bb2-79dd-4841-baa5-298eff79fb5b" />  

## c) Tarkastellaan tallenettuja tietoja
Komennoilla `hosts` ja `services` nähdään, että porttiskannaus tallentui tietokantaan.  
<img width="915" height="667" alt="image" src="https://github.com/user-attachments/assets/35b07ccf-5073-4db5-851a-0957f1f82dcd" />  
Komennolla `services -p 21` saadaan suodatettua vain portti 21.  
<img width="617" height="166" alt="image" src="https://github.com/user-attachments/assets/47e87f2c-a839-47ea-b814-ab597e793eff" />  
Komennolla `services -s http` saa näkyviin molemmat http portit.  
<img width="778" height="141" alt="image" src="https://github.com/user-attachments/assets/8dc3ba1a-02bf-4380-bf18-fad22d6d155d" />  

## d) Internet famous  
Yksi tunnettu hyökkäys on portissa 21 oleva vsftpd. Se löytyi komennolla `search vsftpd`.
<img width="1029" height="199" alt="image" src="https://github.com/user-attachments/assets/e51aad83-6722-4627-869a-da5540983b4b" />  

## e) Nmapin oma tiedoston tallennus VS db_nmap.  
`nmap -oA foo 192.168.56.11` komento tallentaa kolme tiedostoa nmapista; foo.nmap, foo.gnmap ja foo.xml.  
<img width="498" height="90" alt="image" src="https://github.com/user-attachments/assets/e67c4e07-bded-4ca0-baf4-ea4b000447ff" />  
Tästä saadaan helpommin suoraan ihmisen luettavaa, kun db_nmap tallentaa tiedot tietokantaan, mistä muut moduulit voivat lukea ne.  

## f) Murtaudu Metasploitablen vsftpd-palveluun  


## Lähteet  
Jaswal, N. 2020. Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit. https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-31  
nmap.org. Nmap Network Scanning / Chapter 15. Nmap Reference Guide. https://nmap.org/book/man-host-discovery.html
