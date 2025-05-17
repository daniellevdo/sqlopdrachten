# Sql basis

### Database gegevens aanpassen
Maak gebruik van het sql-bestand idscan.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Queries winkelketen
* Welke medewerkers (id, voornaam, achternaam)zijn er in dienst van de winkelketen.
SELECT `id`,`firstname`,`lastname` FROM persons; 

* Hoeveel medewerkers hebben dezelfde functie (jobtitle)
SELECT jobtitle, COUNT(*) AS aantal_functies FROM persons GROUP BY jobtitle; 

* Hoeveel medewerkers zijn professor of ingenieur (title = prof, ir of ing)
SELECT title, COUNT(*) AS aantal_prof_ir_ing FROM persons WHERE title IN ('ing.', 'ir.', 'prof.'); 
GROUP BY title; -- optioneel per groep

* Overzicht van medewerkers (id, voornaam, tussenvoegsel, achternaam) per gebouw (buildingname, street en buildingnumber)
/

* Overzicht van medewerkers (id, voornaam, tussenvoegsel, achternaam) die op een *  * bepaalde datum in gebouw met id 1 waren (buildingname, 

SELECT p.id, p.firstname, p.lastname FROM persons p JOIN scans s ON p.id = s.person_id WHERE s.scandate = "23-09-14" AND s.building_id = 1;

* Overzicht van medewerkers die op diezelfde datum vergeten zijn om uit te checken

SELECT DISTINCT p.id, p.firstname, p.lastname FROM persons p JOIN scans s_in ON p.id = s_in.person_id WHERE s_in.scandate = '2023-09-14' AND s_in.in_out = 'in' AND NOT EXISTS ( SELECT 1 FROM scans s_out WHERE s_out.person_id = s_in.person_id AND s_out.scandate = s_in.scandate AND s_out.in_out = 'out' ); 

* Overzicht van het aantal medewerker per gebouw op 13 september 2023.
SELECT b.buildingname, b.street, b.buildingnumber, COUNT(DISTINCT s.person_id) AS aantal_medewerkers FROM scans s JOIN buildings b ON s.building_id = b.id WHERE s.scandate = '2023-09-13' GROUP BY s.building_id, b.buildingname, b.street, b.buildingnumber; 

* Overzicht van medewerkers en het aantal uur dat ze op 15 september 2023 hebben gewerkt.
SELECT p.id, p.firstname, p.lastname, SEC_TO_TIME( TIMESTAMPDIFF(SECOND, MIN(CASE WHEN s.in_out = 'in' THEN CONCAT(s.scandate, ' ', s.scantime) END), MAX(CASE WHEN s.in_out = 'out' THEN CONCAT(s.scandate, ' ', s.scantime) END) ) ) AS gewerkte_tijd FROM persons p JOIN scans s ON p.id = s.person_id WHERE s.scandate = '2023-09-15' GROUP BY p.id, p.firstname, p.lastname; 

* Medewerker van de maand! (De medewerker die het meeste uren heeft gemaakt van iedereen in de maand september)
SELECT p.id, p.firstname, p.lastname, SEC_TO_TIME(SUM(d.gewerkte_seconden)) AS totaal_gewerkte_tijd FROM persons p JOIN ( SELECT s.person_id, s.scandate, TIMESTAMPDIFF(SECOND, MIN(CASE WHEN s.in_out = 'in' THEN CONCAT(s.scandate, ' ', s.scantime) END), MAX(CASE WHEN s.in_out = 'out' THEN CONCAT(s.scandate, ' ', s.scantime) END) ) AS gewerkte_seconden FROM scans s WHERE s.scandate BETWEEN '2023-09-01' AND '2023-09-30' GROUP BY s.person_id, s.scandate ) d ON p.id = d.person_id GROUP BY p.id, p.firstname, p.lastname ORDER BY SUM(d.gewerkte_seconden) DESC LIMIT 1; 