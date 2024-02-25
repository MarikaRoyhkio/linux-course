## Linux kurssin kotehtävä 5 "Koko juttu"

### Virtuaalikoneen asennus  ja käyttöönotto

Virtuaalikone asennetaan kannettavall Lenovo IdePad5 tietokoneelle, jossa on Windows 10 käyttöjärjestelmä.

#### Uuden virtuaalikoneen luonti:

   - Virtuaalikoneen nimen valinta.

   - ISO-imagen valinta (Debian)
      - 64 bit versio
      - skip unattented instaolation

   - Hardwaren valinta:
        - base = 7500MB 
        - CPU = 4 
        - hard disc = 60,0 GB
      - Ei valita 'Pre-allocate full size'

   - Käynnistetään virtuaalikone. Kone ei näytä minkäänlaisia erroreita, ja noin 10 minuutin odottelun jälkeen näkyviin tulee virtuaalikoneen työpöytä

   - Työpöydältä valitaan ”Install debian”
   
   - Ponnahdusikkunasta valitaan ”launch anyway”

   - Kieleksi valitaan ”American english”

   - Aikavyöhykkeeksi valitaan suomi klikkaamalla maata kartasta

   - Näppäimistöksi valitaan myös suomi
        -  ensimmäisestä valinnasta ”Finnish”
        - tokasta ”Default”

   - VBOX harddisk
       - valitaan ”Erase disk”
       - sijainnit jätetään oletusarvoisiksi

   - Annetaan nimi, login nimi ja tietokoneen nimi sekä salasana

   - Klikataan näytön yläreunasta kokopainiketta, jotta sadaaan näkyviin ”finish”. Tarkistetaan tiivistelmä, ja asennetaan
       - asennuksen kesto oli noin 23 minuuttia


   - Ohjelma kysyy 'Restart now' -> yes

   - Pienen näytön vilkuttelun jälkee, pyytää kirjautumaan sisään.
       - Tsisäänkirjautumisen jälkeen vielä testataan koneen toimivuus avaamalla selain: aukeaa

#### APACHEN ASENNUS

      $ sudo apt-get update
      $ sudo apt-get install apache2

#### Palomuurin asennus:

      $ sudo apt-get update
      $ sudo apt-get install ufw

##### Jätetään porteille tilat palomuuriin:      
      $ sudo ufw allow 22/tcp
      $ sudo ufw allow 80/tcp
      $ sudo ufw enable

##### Apachen uudelleenkännistys:
      $ sudo systemctl restart apache

#### SSH-ASENNUS
      $ sudo apt-get update
      $ sudo apt-get istall openssh-server

#### Muokataan Apachen etusivu:
      $ etc/apache2/sites-available/kukkapurkki.conf
   
   - lisätään tiedostoon 

    <VirtualHost *:80>
       ServerName www.kukkapurkki.com
       DocumentRoot /var/www/kukkapurkki
          <Directory /var/www/kukkapurkki>
             Options Indexes FollowSymLinks
             AllowOverride None
             Require all granted
             Allow from all
          </Directory>
    </VirtualHost>

   - Uudelleenkäynnistetään apache:

    $ sudo systemctl restart apache2

   - Loin HTML – tiedoston korvaamaan alkuperäisen index-sivun:

    $ nano aloitussivu.html

    <!DOCTYPE html>
    <html lang="fi">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Tehtävä 5</title>
    </head>
    <body>

        <header>
            <h1>Tehtävä 5</h1>
        </header>

        <main>
            <p style="font-size: smaller;">Uusi etusivu Linux-kurssin kotitehtävään "Koko juttu"</p>
        </main>

       

   - Tämän jälkeen korvasin alkuperäisen index tiedoston:
        sudo mv aloitussivu.html /var/www/html/index.html

   - Tämän jälkeen tekemäni html sivu näkyi, kun hain selaimessa localhostia. Kuitenkaan aiemmin määrittämäni kukkapurkki.com sivu ei näkynyt jostain syystä?

#### SSH-kirjautumisen automatisointi

      $ ssh-keygen -t rsa -b 2048

   - enteriä, jolloin tallentuu oletussijaintiin

    $ passhphrase:


   - avain tallennettiin

    $ ssh-copy-id marikav@palvelimenIP

   - tarkistetaan, että avain on tallentunut:

    $ ssh marikav@ip-osoite¨

   - tarkistetaan lisätyt avaimet:

    $ cat ~/.ssh/authorized_keys

#### Digging host

Valitettavasti edelliselle viikolle vuokraamani Domain ei ole käytössä enää. Ongelma on selvityksessä namecheapin ja DigitalOceanin kanssa. Tehtävien deadline tuli kuitenkin ennen kuin ongelma saatiin selvitettyä, joten käytin 'host' ja 'dig' komentoja terokarvinen.com sivuun.

    $ host terokarvinen.com

terokarvinen.com has address 139.162.131.217
terokarvinen.com mail is handled by 10 mx.runbox.com.

    $ dig terokarvinen.com

    ; <<>> DiG 9.18.24-1-Debian <<>> terokarvinen.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34837
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 4096
    ;; QUESTION SECTION:
    ;terokarvinen.com.   	 IN    A

    ;; ANSWER SECTION:
    terokarvinen.com.    9313    IN    A    139.162.131.217

    ;; Query time: 4 msec
    ;; SERVER: 192.168.10.1#53(192.168.10.1) (UDP)
    ;; WHEN: Sun Feb 25 19:01:47 EET 2024
    ;; MSG SIZE  rcvd: 61

##### 'dig'-komennon tulos purettuna:

   - "terokarvinen.com" -domainin IPv4-osoite on 139.162.131.217. 
   - TTL (time-to-live) on 9313 sekuntia:

    terokarvinen.com. 9313 IN A 139.162.131.217

   - DNS-viestin lisäominaisuudet:
     
    OPT PSEUDOSECTION:
    EDNS: version: 0, flags:; udp: 4096

   - Kyselyaika oli 4 millisekuntia
   - Vastanneen DNS-palvelimen IP-osoite on 192.168.10.1 ja se käyttää porttia 53:

    ;; Query time: 4 msec
    ;; SERVER: 192.168.10.1#53(192.168.10.1) (UDP)
    
   - Kysely tehtiin aikaan Sun Feb 25 19:01:47 EET 2024
   - Kyselyllä saadun vastauksen koko oli 61 tavua:

    ;; WHEN: Sun Feb 25 19:01:47 EET 2024
    ;; MSG SIZE rcvd: 61


   - Yhteenvetona:
      - "terokarvinen.com" IPv4-osoite on 139.162.131.217
      - vastaus kyselyyn saatiin 4 millisekunnissa
      - Kysely tehtiin DNS-palvelimelle IP-osoitteessa 192.168.10.1.




