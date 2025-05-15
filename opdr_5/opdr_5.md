# Sql basis

### Database
Maak gebruik van het sql-bestand flits.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries flitspaal
* Welke cameras zijn er en waar staan ze (id, address, city, max_speed).
SELECT id, address, city, max_speed FROM cameras; 

* Overzicht van boetes op 50km wegen
SELECT * FROM `flashes` WHERE `camera_id` IN (7, 8, 13, 14, 16, 17, 18); 

* Overzicht van overtredingen van 1 kenteken.
SELECT * FROM `flashes` WHERE `license` = '0-LCL-93'; 

* N.a.w.-gegevens van de hardrijders die het meest in de fout zijn gegaan. (top 10)
SELECT l.first_name, l.last_name, l.address, l.postal_code, l.city, COUNT(f.id) AS number_of_flashes FROM licenses l JOIN flashes f ON l.license = f.license GROUP BY l.license, l.first_name, l.last_name, l.address, l.postal_code, l.city ORDER BY number_of_flashes DESC LIMIT 10; 

* Welke camera’s (id, address, city) meten de meeste snelheidsovertredingen (top 10)
SELECT c.id, c.address, c.city, COUNT(f.id) AS number_of_flashes FROM cameras c JOIN flashes f ON c.id = f.camera_id GROUP BY c.id, c.address, c.city ORDER BY number_of_flashes DESC LIMIT 10;


* Welke auto’s (kenteken, merk, type) zijn het meeste geflitst


* Welke flitspaal (=camera met id, address, city) flitst het meest (top 10)
zelfde als 2 hierboven?


* Kentekens van auto’s die het hoogste bedrag aan boetes hebben gekregen (top 10)


* Overzicht van auto’s (kenteken, merk, type) waarvan het kenteken overeenkomt met sitecode 10 (zoals X-999-XX) https://nl.wikipedia.org/wiki/Nederlands_kenteken.
