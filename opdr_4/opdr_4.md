# Sql basis

### Database 
Maak gebruik van het sql-bestand reisbureau.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries reisbureau
* Geef de namen van de klanten die in Rotterdam wonen
SELECT * FROM `klanten` WHERE `Plaats` = 'Rotterdam'; 

* Geef de namen van de klanten die geen reis geboekt hebben.
SELECT k.Naam FROM klanten k LEFT JOIN boekingen b ON k.Klantnummer = b.Klantnummer WHERE b.Klantnummer IS NULL; 

* Hoeveel klanten komen er niet uit Rotterdam

SELECT COUNT(*) AS aantal_niet_rotterdam FROM `klanten` WHERE `Plaats` <> 'Rotterdam'; 

* Hoeveel reizen hebben als bestemming Afrika?
SELECT COUNT(*) AS aantal_afrika
FROM bestemmingen
WHERE Werelddeel = 'Afrika';
 

* Hoeveel moeten de klanten, die naar Azië gaan, in totaal betalen?


* Geef de namen van de klanten die met kinderen op reis gaan.


* Hoeveel verschillende reizen kun je boeken bij dit reisbureau?


* Geef de naam en postcode van de klanten die in een postcode gebied wonen dat begint met een 9.


* Groepeer de klanten op woonplaats. Geef de woonplaats en het aantal klanten per woonplaats.


* Geef naam en datum van de klanten die voor de maand April een reis hebbben geboekt.


* Geef de namen van klanten, het werelddeel van de bestemming en het aantal dagen van de reis voor boekingen van minimaal 15 dagen.
