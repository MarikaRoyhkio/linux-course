## Linux läksyt h2 'Komentaja Pingviini'

### Tehtävä x: tiivistelmä luetusta artikkelista
#### 'Command Line Basics Revisited'

- Linuxin ja BSD:n komentorivi on ollut olemassa ennen Googlea, webiä, Linuxia, Windowsia ja internetiä.
- Kometorivin käyttäjä vuorovaikuttaa symbolilla "$". Käyttäjä ei kirjoita merkkiä itse
- Peruskäskyjä ovat muun muassa:
  - 'pwd' (tulosta työhakemisto) 
  - 'ls' (listaa tiedostot)
  - 'cd' (vaihda hakemistoa)
  - 'less' (tiedoston tarkastelu
- 'man'-komento näyttää käskyjen erilliset ohjesivut ja '--help' tarjoaa lyhyen avun joillekin käskyille
- 'help' komento avaa lyhyen ohjeistuksen suoraan komentorivillä, ’man’ avaa pidemmän manuaalin less-tilassa
- Tärkeitä hakemistoja ovat esimerkiksi ’home’, ’etc’, ’media’ ja ’var/log’, joilla on erityiset tarkoitukset.
  - nämä hakemistot löytyvät ja ovat samanlaiset kaikissa Linux-systeemeissä

#### Kokeilua vaativia tehtäviä paremmin demonstroivien kuvakaappausten tallennus epäonnistui, jota en huomannut ajallaan. Tämän vuoksi melkein koko raportti on vain tekstimuodossa / kuvissa näkyvät kellonajat eivät täsmää kirjallisen raportin aikaleimoihin

 ### Tehtävä a: Micro
 Kuten kaikki myöhemmätkin tehtävät, tämä on toteutuettu Lenovo Ideapad 5 Pro tietokoneelle asennetulla virtuaalikoneella. 

19:27 avasin Applications-valikosta "Terminal emulator" ohjelman

19:28 Etsin tietoa Micro:n asnetamisesta (https://terokarvinen.com/2022/command-palette-cheatsheet-run-and-make-micro/)

19:30 Olemassa olevien tiedostojen päivitys: "sudo apt-get update"

19:30 Micron asennus: "sudo apt-get install micro"

19:32 Micron testaus: "micro TEKSTIA.txt". Komento acvasi editorin, jolla pystyin luomaan ja tallentamaan tekstitiedoston nimellä "TEKSTIA"

 ### Tehtävä b: Rauta
 19:45  Asensin lshw:n : "sudo apt install lshw"
 
 19:47 Listasin koneen raudan: "sudo lshw -short -sanitize"

Tämä listaus esittää tietokoneen laitehierarkian tai laitteiston tiedot. Kunkin rivin tarkoitus on kuvata eri laitteita ja komponentteja tässä tietokoneessa, ja siinä toimivassa virtuaalikoneessa.
- Yleinen tieto: VirtualBox-ympäristö

- Prosessointi: AMD Ryzen 7 5800H with Radeon Graphics -prosessori. Tämä näyttäisi olevan sama kuin oikeassa kannettavassa, jolle virtuaalikone on asennettu

- Muisti: 7552 megatavua järjestelmän muistia.

- Näyttö:SVGA II Adapter -näyttö

- Verkkokortti: 82540EM Gigabit Ethernet Controller

- Äänikortti: AC'97 Audio Controller, joka vastaa äänentoistosta.

- SATA-tallennusohjain: 82801HM/HEM (ICH8M/ICH8M-E) SATA Controller. Hallitsee tallennuslaitteita, kuten kiintolevyä.

- Kiintolevy: 59GB VBOX HARDDISK, jossa on kaksi osiota. Tämä on virtuaalikoneen kiintolevy.
USB-liitännät

- Tulo- ja lähtötasot:

    - Näppäimistö

    - Hiiri

    - Virtapainike, Video Bus, Sleep Button, PC Speaker ja muut laitteet.


 ### Tehtävä c: APT

 20:00 cowsay:n asennus: "sudo apt install cowsay"

  - komento asentaa ohjelman, jolla pystyy luomaan "puhuvan lehmän" komentorivityökaluun.
 
 20:01 cowsay:n testaus : "cowsay "puhuva lehmä"

![cowsay puhuva lehmä](IMG20240128232956.jpg)

 20:05 lolcat:in asennus: "sudo apt install lolcat"

  - lolcat vaihtaa koentorivin tekstin värin sateenkaaren kirjavaksi
   
 20:05 lolcat:in kokeilu: "lolcat -h"
 
 ![lolcat esimerkki](IMG20240128233357.jpg)

 20:10 oneko:n asennus: "sudo apt install oneko"

  - oneko asentaa komentoriviin pienen kissan, joka juoksee kursorin perässä
     
 20:11 oneko:n kokeilu: "oneko"
 
 ![oneko](VID20240128200855[1].gif)

 Huomasin vasta tässä viheessa loput tehtävänannosta, joten en tullut kokeilleeksi asentaa kaikkia samaan aikaan. Epäilisin kuitenkin että "|" - merkillä esimerkiksi olisin voinut tässä onnistua.

 ### Tehtävä d: FHS

 En saanut tämän tehtävän ideasta kiinni. Pystyin kyllä hyppäämään noissa "Command Line Basics Revisited" kappaleessa listatuissa kansioissa edestakaisin niiden välillä, mutta VirtualBox ei näyttänyt että niissä olisi ollut mitään? Komentorivi ei antanut virheilmoituksia, se vain pyysi uutta komentoa. 

 ### Tehtävä e: The friendly M

 Grep-komentojen testaamista varten loin erillisen tekstitiedoston, "esimerkki.txt"
 
 ![esimerkkikansio](IMG20240128234806.jpg)

 20:30 Grepin testaaminen: "grep "esimerkki" esimerkki.txt
   -komento tulostaa valitusta kansiosta kaikki rivit, joilla mainitaan sana "esimerkki"

 20:32 Toisen Grep-komennon testaaminen: "grep "esimerkki" esimerkki.txt > tulos.txt"
   -komento kopioi "esimerkki.txt" kansiosta kaikki rivit, joilla mainitaan sana "esimerkki" kansioon nimeltä 
    "tulos.txt". Tässä tapauksessa kansiota "tulos.txt" ei ollut vielä olemassa, joten komento loi sen erikseen

Grep-komennolla voi siis esimerkiksi etsiä ja käyttää tiedostoja ja kansioita ja niiden sisältöjä

  ### Tehtävä f: Pipe
  
Etsin "esimerkki.txt" kansiosta kaikki rivit, jotka sisältävät kirjaimen e, ja lajittelin ne aakkosjärjestykseen rivinen ensimmäisen kirjaimen mukaan: " grep "e" esimerkki.txt | sort

Putkilla voi siis yhdistää ja "jonottaa" komentoja

 ### Tehtävä g: Tukki

 Sain komentosarjalla tehtyä komentoja, jotka toimivat kuten kuului, ja komentoja, jotka eivät onnistu syystä tai toisesta. Lokitietojen hakemisessa on tämän paremmin onnistunut, useammasta yrityksestä huolimatta? En saa tästä analysoitua muuta, kuin että jotain USB laitteen tietoja se pyörittää ja tunnistaa 

  [sudo] password for marikar:
  tammi 28 21:00:37 floravb kernel: usb 2-1: USB disconnect, device number 31
  
  tammi 28 21:00:38 floravb kernel: usb 2-1: new full-speed USB device number 32 using ohci-pci
  
  tammi 28 21:00:39 floravb kernel: usb 2-1: New USB device found, idVendor=80ee, idProduct=0021, bcdDevice= 1.00
  
  tammi 28 21:00:39 floravb kernel: usb 2-1: New USB device strings: Mfr=1, Product=3, SerialNumber=0
  
  
  tammi 28 21:00:39 floravb kernel: usb 2-1: Product: USB Tablet
  
  tammi 28 21:00:39 floravb kernel: usb 2-1: Manufacturer: VirtualBox
  
  tammi 28 21:00:39 floravb kernel: input: VirtualBox USB Tablet as /devices/pci0000:00/0000:00:06.0/usb2/2-1/2- 
  1:1.0/0003:80EE:0021.001F/input/input38
  
  tammi 28 21:00:39 floravb kernel: hid-generic 0003:80EE:0021.001F: input,hidraw0: USB HID v1.10 Mouse 
  [VirtualBox USB Tablet] on usb-0000:00:06.0-1/input0
  
  tammi 28 21:01:01 floravb sudo[5981]:  marikar : TTY=pts/0 ; PWD=/home/marikar ; USER=root ; 
  COMMAND=/usr/bin/journalctl -f
  
  tammi 28 21:01:01 floravb sudo[5981]: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=1000)

  

