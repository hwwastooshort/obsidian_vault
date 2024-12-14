- Schema der Datenbank 
![[Bildschirmfoto 2024-12-08 um 10.36.59.png]]
- Geben Sie Namen von Künstlern mit Herkunftsland Germany sortiert nach ArtistId aus
```sql
SELECT Name
FROM Artitsts
WHERE Location = 'Germany'
ORDER BY ArtistId
```
- Geben Sie Jahre, in denen ein Album mit dem Namen "Best of" veröffentlicht wurde, absteigend sortiert aus
```sql
SELECT Year
FROM Records 
WHERE Name = 'Best of'
ORDER BY Year DESC
```
- Geben Sie die Namen von Alben aus, die ein Künstler namens Pink Floyd veröffentlicht hat
```sql
SELECT Records.Name
FROM Artists
JOIN Records ON Artists.ArtistId = Records.ArtistId
WHERE Artists.Name = 'Pink Floyd'

SELECT r.Name
FROM Records r, Artists a
WHERE r.ArtistId = a.ArtistId AND a.Name = 'Pink Floyd'
```
- Geben Sie das früheste und späteste Jahr aus, indem ein Album mit dem Titel 'Best of' veröffentlicht wurde
```sql
SELECT MIN(Year), MAX(Year)
FROM Records
WHERE Name = 'Best of'
```
- Geben Sie die Namen von Künstlern mit bekanntem Geschlecht aus, die aus Norwegen oder Schweden stammen
```sql
SELECT Name
FROM Artists
WHERE Gender IS NOT NULL 
AND Location IN ('Norway', 'Sweden')
```
- Geben Sie Jahre aus, in denen sowohl ein Album von The Beatles als auch ein Album von The Rolling Stones erschienen ist
```sql
SELECT DISTINCT Records.Year
FROM Records
JOIN Artists ON Records.ArtistId = Artists.ArtistId
WHERE Artists.Name = 'The Beatles'

INTERSECT

SELECT DISTINCT Records.Year
FROM Records
JOIN Artists ON Records.ArtistId = Artists.ArtistId
WHERE Artists.Name = 'The Rolling Stones'

--Alternative, schlechtere Lösung

SELECT DISTINCT r1.Year
FROM Artists a1, Records r1, Artists a2, Records r2
WHERE a1.ArtistId = r1.ArtistId AND a1.Name = 'The Beatles'
AND a2.ArtistId = r2.ArtistId AND a2.Name = 'The Rolling Stones'
AND r1.Year = r2.Year
```
