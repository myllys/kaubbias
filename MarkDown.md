## Palvelimet Spring 2021 h3-Versionhallinta myllys

# Tämä kotitehtävä on raportti kurssin harjoitukseen 3 - [versionhallinta](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/#h3-versionhallinta)

Käytän harjoituksessa omaa pöytäkonetta, jossa Windows 10, johon on asennettu VirtualBox 6.1.16 r140961,
VirtualBoxissa käyttöjärjestelmänä Ubuntu 20.04 LTS

Aloitan raportoinnin 20.04.2021 KLO 12:45

a) MarkDown. Tee tämän tehtävän raportti MarkDownina. Helpointa on tehdä raportti GitHub-varastoon,
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
