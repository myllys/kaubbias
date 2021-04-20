## Palvelimet Spring 2021 h3-Versionhallinta myllys

# Tämä kotitehtävä on raportti kurssin harjoitukseen 3 - versionhallinta / lisää linkki

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

b) Näytä omalla git varastollasi esimerkit komennoista 'git log', 'git diff' ja 'git blame'

Repossa kirjoitan komennon git log

	git log
