# Sql basis

### Database gegevens aanpassen
Maak gebruik van het sql-bestand reisbureau.sql en voer hierop onderstaande opdrachten uit.
Theorie kun je vinden op: https://www.edutorial.nl/dbq/introductie/

### Opdracht 1
* Geef de query om alle tabellen in de database 'reisbureau' weer te gegeven
```sql
SHOW TABLES; 
````

### Opdracht 2
* Voeg 2 nieuwe klanten toe aan de tabel 'customers' (je mag de waarden zelf bedenken)

INSERT INTO customers (
    first_name, last_name, email, address, postal_code, city, country_code, phone
)
VALUES (
    'usha123', 'Barf', 'jan@example.com', 'poepershoek 4', '1234 AB', 'Zwolle', 'da_DK', '0612345678'
),
VALUES (
    'piet123', 'Koekje', 'pan@example.com', 'poepershoek 12', '1235 AB', 'Zwolle', 'da_DK', '0612345678'
);

### Opdracht 3
* Geef de query om de eerste 10 boekingen te verwijderen (reservations)

DELETE FROM reservations
ORDER BY id
LIMIT 10;

### Opdracht 4
* De klant met id 13 is verhuist naar 'De van der veldensteeg 81' in 'Apeldoorn'.
* Pas het record aan en geef de query
* Toon het record en controleer of de gegevens correct zijn.

UPDATE customers
SET city = 'Apeldoorn', address = 'De van der veldensteeg 81'
WHERE id = 13;
