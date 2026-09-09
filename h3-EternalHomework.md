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




## Lähteet  
Jaswal, N. 2020. Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit. https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-31  
nmap.org. Nmap Network Scanning / Chapter 15. Nmap Reference Guide. https://nmap.org/book/man-host-discovery.html
