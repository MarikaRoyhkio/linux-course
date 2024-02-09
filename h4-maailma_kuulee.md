## Tehtävä x: Tiivistelmä luetuista artikkeleista

### Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4)

a)
- GitHub Education-paketilla opiskelija voi saada palvelimen ja domainnimen käyttöönsä ilmaiseksi
- Digital Ocean kerää maksutiedot henkilöllisyyden varmistamiseksi
- Domain nimen saa vuokrattua NameCheapilta
    - .me päätteisen nimen saa ilmaiseksi GitHubin Education paketin avulla
d)
- virtuaalipalvelinta ensimmäistä kertaa käytettäessä päivitysten tiedot haetaan koneen terminaalissa komennolla

       $ sudo apt-get update
- Palomuuri asennetaan komennolla

      $ sudo apt-get install ufw
   - palomuuriin tehdään reikä porttia varten komennolla
   
         $ sudo ufw allow 22/tpc
   - palomuuri laitetaan päälle
   
         $ sudo ufw enable
e)
- virtuaalipalvelimen käyttäjä luodaan terminaalissa komennolla

       $ sudo adduser + valitsemasi käyttäjänimi
- virtuaalipalvelimelle käyttäjää luodessa tietoja täyttäessä riittää nimen täyttäminen, muut kohdat voi jättää tyhjäksi
f)
- palvelimen ohjelmien saatavilla olevat päivityksen voi hakea komennolla

      $ sudo apt-get update
- palvelimen saatavilla olevat asetukset voi asentaa komennolla

      $ sudo apt-get upgrade
- palvelimen tietoturvapäivitykset voi asentaa komennolla

      $ sudo apt-get dist-upgrade

### First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS

-	virtuaalipalvelinta luodessa on hyvä valita palvelinkeskus, joka on lähellä omaa sijaintia (esimerkiksi Euroopassa)
-	ennen nimen vuokraamista, palvelimen voi löytää selaimessa IP osoitteella
- oikeaa nimeä on kuitenkin helpompi hakea kuin pitkää numerosarjaa

## Tehtävät a, b, c ja d


17:48

Lähdin hakemaan GitHub Education pakettia, joilla saisin määräaikaisesti ilmaisen domain-nimen ja verkkopalveimen. Täytin ja tallensin tietoni, ja sain ilmoituksen, että saisin yhteydenoton GitHubilta liittyen Education pakettiin ”tunnin tai viimeistään 7 päivän kuluessa”. Lopulta kävi niin, että ei se ainakaan tunnissa tullut, joten jatkoin tehtävien tekemistä ilman sitä.

19:37 Minulla oli jo DigitalOceanin tunnukset, vaikken ole sillä ennen mitään tehnyt. Tällä kertaa valitsin ”Deploy virtual machine”

<img src="Näyttökuva 2024-02-09 194155.png" alt="kuva" style="height: 500px; width:700px;"/>

Alueeksi valitsin sen, mikä on suositellusti lähimpänä sivun käyttäjiä, eli Euroopassa.

<img src="Näyttökuva 2024-02-09 194215.png" alt="kuva2" style="height: 500px; width:700px;"/>

Seuraavaksi valitsin Debianin, sillä sitä käytän virtuaalikoneellani

<img src="Näyttökuva 2024-02-09 194253.png" alt="kuva3" style="height: 500px; width:700px;"/>

Tyypiksi valitsin halvimmat, basic type (shared cpu)

<img src="Näyttökuva 2024-02-09 194343.png" alt="kuva4" style="height: 500px; width:700px;"/>

Salauksen otin salasanalla

<img src="Näyttökuva 2024-02-09 194522.png" alt="kuva5" style="height: 500px; width:700px;"/>

Hostname ei liity varsinaisesti mihinkään, mutta on muidenkin silmille sopiva.

19:45 Seuraavaksi avasin virtuaalikoneen, ja yhdistin sen verkkopalvelimeen komentorivissä komennolla
    
    ssh root@verkkopalvelimen IP osoite

Seuraavaksi asensin palomuurin käyttäen seuraavia komentoja, alla mainitussa järjestyksessä:
    
    sudo apt-get update
    sudo apt-get install ufw
    sudo ufw allow 22/tcp
    sudo ufw enable
    sudo ufw status

Seuraavaksi loin käyttäjän:
    
    sudo adduser marikar

Asetin käyttäjälle salasanan, ja täytin koemntorivin kysymistä tiedoista vain nimen.
    
    sudo adduser marikar sudo

Tässä vaiheessa avasin toisen terminaalin päällekkäin tämän kanssa. siirryin käyttämään vuokraamani palvelinta komennolla
    
    ssh marikar@ip osoite

Asetin salasanan. Tämän jälkeen testasin toimivuutta komennolla
    
    sudo echo ”Moi”

Lukitsin root-tunnuksen  komennolla 
    
    sudo usermod –lock root

Päivitin kaikki paketit. Seuraavaksi asensin apachen:
    
    sudp apt-get install apache2

Selain löysi localhost sivun IP-osoitteella

<img src="Näyttökuva 2024-02-09 203914.png" alt="kuva6" style="height: 500px; width:700px;"/>

20:01 Seuraavaksi korvasin oletussivun omalla sivullani:

Loin uuden HTML-sivun komennolla
   
    nano aloitussivu.html

Kirjoitin HTML5 sivun, jossa on otsikko, sekä tekstiä. Tallensin tiedoston. Seuraavaksi korvasin ”index.html” tiedoston juuri äsken luomallani tiedostolla komennolla
    
    sudo mv aloitussivu.html /var/www/html/index.html

Uudelleenkäynnistin apachen komennolla
    
    sudo systemctl restart apache2

Testasin, toimiko muutos hakemalla sivua nettiselaimella palvelimen IP-osoitteella. Pyysin myös puolisoani testaamaan omalla kännykällään, näkyykö itse kirjoittamani sivu. 
Seuraavaksi vuokrasin domain-nimen namecheap.com osoitteesta. Valkkasin tässä vaiheessa halvimman mahdollisen vaihtoehdon, joka päätyi olemaan .online . En ottanut sille mitään lisäpalveluita, ja otin auto-renew ominaisuuden pois päältä.
Yhdistin palvelimeni IP-osoitteen domain-nimeen siirtymällä Namecheap:in dashboardille, ja valitsemalla sieltä ”Domain list” vaihtoehdon. Seuaavaksi valitsin kohdan ”Advanced DNS”. Poistin kaikki valmiina olleet tiedot kohdasta ”Host records”, ja korvasin ne luomalla tiedostot oman palvelimeni IP osoitteella. Noin tunnin kuluttua testasin hakea muutamalla eri laitteella osoitetta ”marikaroyhkio.online”. Haku päätyi onnistuneesti omalle sivulleni.
