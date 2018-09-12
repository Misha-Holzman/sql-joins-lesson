## Further Lab

- first clone this repo
- Navigate to `spots`
-  `createdb musicdb`
- `psql -d musicdb -f seed.sql`

Then do the following:



<!-- - Identify all relations/constraints on the track table, are there any others? -->

Foreign-key constraints:
    "track_album_id_fkey" FOREIGN KEY (album_id) REFERENCES album(id)
    "track_artist_id_fkey" FOREIGN KEY (artist_id) REFERENCES artist(id)
Referenced by:
    TABLE "likes" CONSTRAINT "likes_track_id_fkey" FOREIGN KEY (track_id) REFERENCES track(id)



<!-- - Find all songs released on albums from the `Interscope` label -->

SELECT disc_number, track.name AS track_name, album.name AS album_name, artist.name AS artist_name
FROM album 
JOIN track ON (track.album_id = album.id) 
JOIN artist ON (track.artist_id = artist.id) 
WHERE album.label = 'Interscope' 
ORDER BY album.name;



<!-- - Find all of Beyoncé's tracks -->

SELECT track.name AS track_name, artist.name AS artist_name
FROM artist
JOIN track ON (track.artist_id = artist.id)
WHERE artist.name = 'Beyoncé'
ORDER BY artist.name;



<!-- - Find all of the disc numbers only for Beyonce's tracks -->

SELECT disc_number, track.name AS track_name, artist.name AS artist_name
FROM artist
JOIN track ON (track.artist_id = artist.id)
WHERE artist.name = 'Beyoncé'
ORDER BY artist.name;



<!-- - Find all of the names of Beyoncé's albums -->

SELECT album.name AS album_name, artist.name AS artist_name
FROM artist
JOIN track ON (track.artist_id = artist.id) 
JOIN album ON (track.album_id = album.id)
WHERE artist.name = 'Beyoncé'
ORDER BY album.name;


<!-- - Find all of the album names, track names, and artist id associated with Beyoncé -->

SELECT artist.id AS artist_id, track.name AS track_name, album.name AS album_name, artist.name AS artist_name
FROM artist
JOIN track ON (track.artist_id = artist.id) 
JOIN album ON (track.album_id = album.id)
WHERE artist.name = 'Beyoncé'
ORDER BY artist.id;



<!-- - Find all songs released on `Virgin Records` that have a `popularity` score > 30 -->

SELECT track.name AS track_name, album.name AS album_name, artist.name AS artist_name, track.popularity AS popularity
FROM album 
JOIN track ON (track.album_id = album.id) 
JOIN artist ON (track.artist_id = artist.id)  
WHERE album.label = 'Virgin Records' AND track.popularity > 30
ORDER BY track.popularity;



<!-- - Find the artist who has released tracks on the most albums
    Hint: The last few may need more than one `join` clause each -->

SELECT COUNT(album) AS number_of_albums, artist.name AS artist_name
FROM artist
JOIN track ON (track.artist_id = artist.id) 
JOIN album ON (track.album_id = album.id)
GROUP BY artist.name
ORDER BY number_of_albums DESC, artist.name DESC








