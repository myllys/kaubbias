## Palvelimet Spring 2021 h3-Versionhallinta myllys

# Tämä kotitehtävä on raportti kurssin harjoitukseen 3 - [versionhallinta](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/#h3-versionhallinta)

Käytän harjoituksessa omaa pöytäkonetta, jossa Windows 10, johon on asennettu VirtualBox 6.1.16 r140961,
VirtualBoxissa käyttöjärjestelmänä Ubuntu 20.04 LTS

Aloitan raportoinnin 20.04.2021 Klo 12:45

a) MarkDown. Tee tämän tehtävän raportin MarkDownina. Helpointa on tehdä raportti GitHub-varastoon,
jolloin md-päätteiset tiedostot muotoillaan automaattisesti. Tyhjä rivi tekee kappalejaon, risuaita otsikon,
sisennys merkitsee koodinpätkän. Vinkkinä artikkeli terokarvinen.com/2016/publish-your-project-with-github/index.html

Aloitin luomalla kaubbias repositoryyn uuden MarkDown tiedoston
	
	sudo nano MarkDown.md

Testinä committaan tämän keskeneräisen raportin virtualboxista githubiin

	git add .

	git commit

Commit messageen kirjoitan "Add MarkDown"

	git pull

Jos muutoksia on tehty otan ne talteen ennenkuin kirjoitan git push komennon

	git push

Push onnistui ongelmitta

![kaubbias](https://user-images.githubusercontent.com/64011606/115380597-676c6980-a1db-11eb-9880-3cab45ed548a.png)

b) Näytä omalla git varastollasi esimerkit komennoista 'git log', 'git diff' ja 'git blame'

Repossa kirjoitan komennon git log

	git log

![git_log](https://user-images.githubusercontent.com/64011606/115380538-558ac680-a1db-11eb-8444-36bf5bc3050a.png)

Lokista näkee että loin tämän repon GitHub sivun kautta, ja lisäsin virtualboxin kautta readme.md tiedoston repoon.
Tein pari testi muutosta lisäämällä tiedoston turvallinen.exe. Nyt kun aloitin kirjoittaa raporttia lisäsin juuri
hetki sitten MarkDown.md tiedoston.

	git diff versio1 versio2

![git_diff](https://user-images.githubusercontent.com/64011606/115381635-6be55200-a1dc-11eb-9fa0-41d31291b0ca.png)

Ensimmäinen muokkaus oli readme.md markdownin kokeilua repossa. Katsoin kahden ensimmäisen version välisiä eroja

	git blame MarkDown.md

![git_blame](https://user-images.githubusercontent.com/64011606/115382195-15c4de80-a1dd-11eb-80b5-cf6599ea288c.png)

Näen kätevästi kaikki esim. markdown tiedostoon tehdyt muutokset ja kuka muutoksen teki.

c) Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset 'git reset --hard'. Huomaa, että tässä toiminnossa ei ole peruutus nappia.

Poistan turvallinen.exe tiedoston
	
	rm turvallinen.exe
	
Kokeilen komentoa
	
	git reset --hard

![git_reset](https://user-images.githubusercontent.com/64011606/115383160-2cb80080-a1de-11eb-93d1-20dd0ef95b08.png)

Kätevä komento jolla saadaan nykyinen repo versio ja sen tiedostot takaisin.

f) Tee uusi salt-moduli. Voit asentaa ja konfiguroida minkä vain uuden ohjelman: demonin, työpöytäohjelman tai komentokehotteesta toimivan ohjelman. Käytä tarvittaessa 'find printf "%T+ "p\n"|sort' löytääksesi uudet asetustiedostot.

	cd /srv/salt
	
Salt kansiossa tehdään ohjelmalle oma kansio, asennan audacity:n joten kansion nimeksi kirjoitan:
	
	sudo mkdir audacity
	
Mennään pois srv/salt kansiosta
	
	cd ..
	
Asennetaan audacity koneeseen komennoilla:
	
	sudo add-apt-repository ppa:ubuntuhandbook1/audacity

Paina enter

	sudo apt-get update

	sudo apt-get install audacity
	
![hidden-files](https://user-images.githubusercontent.com/64011606/115387605-9a1a6000-a1e3-11eb-9f24-a0a4856a9229.png)	

Varmista että show hidden files on päällä

mene kotikansioosi

	cd /home/käyttäjä

Omassa tapauksessa

	cd /home/myllys

![audacity_data](https://user-images.githubusercontent.com/64011606/115387880-e9609080-a1e3-11eb-9433-5ac0f40d6b03.png)

Etsitään asetustiedostot komennolla

	find .audacity-data -printf '%T+ %p\n'|sort
	
Löytyi konfiguraatio tiedosto .audacity-data/audacity.cfg
	
Luodaan tilatiedosto audacitylle

	sudoedit /srv/salt/audacity/audacity.sls
	
Sisällöksi

audacity:
  pkg.installed
/home/myllys/.audacity-data/audacity.cfg:
  file.managed:
    - source: salt://audacity/audacity.cfg

Kopioidaan tiedosto audacity.cfg /srv/salt/audacity kansioon

	sudo cp /home/myllys/.audacity-data/audacity.cfg /srv/salt/audacity/audacity.cfg
	
Muokataan salt audacity konfiguraatiota

	sudo nano /srv/salt/audacity.cfg

Esim muutetaan kohta AudioTimeFormat=hh:mm:ss > AudioTimeFormat=mm:hh:ss nyt minuutit näkyy ennen tunteja

	sudo salt '*' state.apply /audacity/audacity
	
![audacity_sls](https://user-images.githubusercontent.com/64011606/115391878-a1903800-a1e8-11eb-81ed-067756eea447.png)

konfiguraatio tiedoston muuttaminen toimii, testataan että pkg installed ja automaatio toimii poistamalla audacity

	sudo apt-get purge audacity
	
Exec uudestaan komento 
	
	sudo salt '*' state-apply /audacity/audacity
	
![uutta_vaan](https://user-images.githubusercontent.com/64011606/115392894-bfaa6800-a1e9-11eb-820d-875803289688.png)

Suoritetaan sama sudo salt testiksi ja muutoksia ei pitäisi tapahtua:

![no_changes](https://user-images.githubusercontent.com/64011606/115393077-f5e7e780-a1e9-11eb-9126-570019c2828e.png)

Tehtävä 3 raportti päättyi: 20.04.2021 Klo 15:15

Lähteet: 

Audacity 2021. Preferences manual. Luettavissa: https://manual.audacityteam.org/man/preferences.html. Luettu: 20.04.2021

Santeri Myllys 2021. Palvelinten hallinta harjoitus 2. Luettavissa: https://myllys.wordpress.com/palvelinten-hallinta-harjoitus-2-spring-2021/. Luettu: 20.04.2021

Tero Karvinen 2016. Publish your project with GitHub. Luettavissa: http://terokarvinen.com/2016/publish-your-project-with-github/index.html. Luettu: 20.04.2021

