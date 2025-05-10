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

te moeilijk. Ik kwam tot dit:
SELECT COUNT(*) AS aantal_azie
FROM bestemmingen
WHERE Werelddeel = 'Azie'
JOIN FROM`boekingen` 

* Geef de namen van de klanten die met kinderen op reis gaan.
SELECT klanten.naam FROM boekingen JOIN klanten ON boekingen.Klantnummer = klanten.Klantnummer WHERE boekingen.`Aantal kinderen` > 0; 

* Hoeveel verschillende reizen kun je boeken bij dit reisbureau?

SELECT COUNT(DISTINCT Bestemmingcode) AS AantalReizen FROM bestemmingen; 

* Geef de naam en postcode van de klanten die in een postcode gebied wonen dat begint met een 9.
SELECT Naam, Postcode FROM klanten WHERE postcode LIKE '9%'; 

* Groepeer de klanten op woonplaats. Geef de woonplaats en het aantal klanten per woonplaats.
SELECT woonplaats, COUNT(*) AS aantal_klanten
FROM klanten
GROUP BY woonplaats;

* Geef naam en datum van de klanten die voor de maand April een reis hebbben geboekt.
SELECT klanten.Naam, boekingen.Boekdatum FROM boekingen LEFT JOIN klanten ON boekingen.Klantnummer = klanten.Klantnummer WHERE boekingen.Boekdatum LIKE '1999-04%'; 

* Geef de namen van klanten, het werelddeel van de bestemming en het aantal dagen van de reis voor boekingen van minimaal 15 dagen.

Te moeilijk. kwam tot zover:

SELECT klanten.Naam, bestemmingen.Werelddeel, reizen.`Aantal dagen`
FROM boekingen
JOIN klanten ON boekingen.Klantnummer = klanten.Klantnummer
JOIN bestemmingen ON reizen.Bestemmingcode = bestemmingen.Bestemmingcode
WHERE CAST(TRIM(reizen.`Aantal Dagen`) AS INT) >= 15;

