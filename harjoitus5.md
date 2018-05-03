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

Muistin, että minulla oli jo valmiiksi varasto, jossa oli osa tehtävään tarvittavista tiedostoista, joten kopioin sen koneelleni

	git clone https://github.com/Vipa94/salttest
