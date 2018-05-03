# Harjoitus 5

Tehtävä on osa Tero Karvisen Palvelinten hallinta -kurssia:
http://terokarvinen.com/2018/aikataulu-%e2%80%93-palvelinten-hallinta-ict4tn022-4-ti-5-ke-5-loppukevat-2018-5p

## b) Julkaise raportti MarkDownilla. Jos käytät GitHub:ia, se tekee muotoilun automaattisesti “.md”-päätteisiin dokumentteihin.

Tehtävässä mainittu raportti on tämä tiedosto. 


Aloitin luomalla GitHubissa Palvelinten hallinta -nimisen varaston, jonka kloonasin koneelleni komennolla:

	git clone https://github.com/Vipa94/Palvelinten-hallinta

Kloonauksen jälkeen siirryin luotuun kansioon ja tein tämän raporttiteidoston. Halutessani päivittää tiedostoa GitHubiin käytän seuraavia komentoja:

	git add .
	git commit

jotta tiedoston uusin versio päivittyisi lokaalisti, jonka jälkeen päivitän version GitHubiin:

	git pull && git push

Päivityksen yhteydessä kysytään GitHubin käyttäjätunnusta ja salasanaa, mutta ensimmäisen kerran jälkeen voi varmistusväliä muuttaa:

	git config --global credential.helper "cache --timeout=3600"

Käyttäjätunnuksen syötettyäni muutokset päivittyvät GitHubiin.



## c) Aja oma Salt-tila suoraa git-varastosta. Voit joko tehdä tilan alusta lähtien itse tai forkata sirottimen.

Tarkoituksenani on ajaa tila, joka asentaa ssh:n ja muokkaa sen porttia. Portti vaihtuu portista 22 porttiin 1234, ja tarvittavat tila- ja konffitiedostot löytyvät minulta virtuaalipalvelimeltani.
Muistin, että minulla oli jo valmiiksi varasto, jossa oli osa tehtävään tarvittavista tiedostoista, joten kopioin sen koneelleni

	git clone https://github.com/Vipa94/salttest

Loin varastoon kansion ssh, jonne loin tiedoston init.sls.
Lisäksi loin  /salttest/srv/salt kansioon top.sls tiedoston. Sen jälkeen tarkistin kansiosta löytyvän skriptin nimen, joka oli test.sh.

Koneeni oli jo asetettuna Saltilla orjaksi itselleen joten kokeilin vain ajaa bash-skriptin ja katsoin mitä tapahtuu

	local:
	----------
	ID: ssh
	Function: pkg.installed
	Result: True
	Comment: The following packages were installed/updated: ssh
	Started: 19:01:10.144979
	Duration: 21133.619 ms
	Changes:   
	----------
	openssh-server:
	----------
	new:
	1:7.2p2-4ubuntu2.4
	old:
	ssh:
	----------
	new:
	1:7.2p2-4ubuntu2.4
	old:
	ssh-server:
	----------
	new:
                      1
	old:
	----------
	ID: /etc/ssh/sshd_config
	Function: file.managed
	Result: True
	Comment: File /etc/ssh/sshd_config updated
	Started: 19:01:31.301528
	Duration: 25.668 ms
	Changes:   
		----------
		diff:     
		---
	## Tässä tapahtui paljon, sillä käyttämästäni sshd_config tiedostosta
	## on poistettu kommentti kentät 
		+++ 

	----------
	ID: sshd
	Function: service.running
	Result: True
	Comment: Service restarted
	Started: 19:01:31.451549
	Duration: 69.806 ms
	Changes:   
	  ----------
		sshd:
		  True

	Summary for local
	------------
	Succeeded: 3 (changed=3)
	Failed:    0
	------------
	Total states run:     3


Asennus toimi, ja sshd_config tiedostokin muuttui, mutta tarkistetaan vielä

	 ssh -p 1234 vili@localhost

Onnistui, portti siis vaihtui porttiin 1234

	The authenticity of host '[localhost]:1234 ([127.0.0.1]:1234)' can't be established.
	ECDSA key fingerprint is SHA256:pTUrVLgXFsSezCXDzAJyEqtwVItPfP6B5e6ISphg61E.
	Are you sure you want to continue connecting (yes/no)?
