# SQL-statements_exercise
exercise in querying Chinook SQLite db

## Requirements
Use the [Chinook Database](https://chinookdatabase.codeplex.com/) and the [DB Browser for SQLite](http://sqlitebrowser.org/) we downloaded in the ERD exercise.

For each of the following exercises, provide the appropriate query.

Keep your successful queries in a `.md` file.

(1) Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```
SELECT FirstName || " " || LastName AS "Full Name", CustomerId, Country 
FROM Customer
WHERE Country != "USA";
```
(2) Provide a query only showing the Customers from Brazil.
```
SELECT * 
FROM Customer
WHERE Country = "Brazil";
```
(3) Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
```
SELECT FirstName || " " || LastName AS "Name", InvoiceId, InvoiceDate, BillingCountry 
FROM Customer
JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId
WHERE Country = "Brazil";
```
(4) Provide a query showing only the Employees who are Sales Agents.
```
SELECT FirstName || " " || LastName AS "Sales Agents" 
FROM Employee
WHERE Title = "Sales Support Agent"
```
(5) Provide a query showing a unique list of billing countries from the Invoice table.
```
SELECT BillingCountry 
FROM Invoice
GROUP BY BillingCountry;
```
(6) Provide a query showing the invoices of customers who are from Brazil.
```
SELECT * 
FROM Invoice
WHERE BillingCountry = "Brazil";
```
(7) Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
```
SELECT Employee.FirstName || Employee.LastName As "Sales Agent", Invoice.* 
FROM Employee
JOIN Customer On Employee.EmployeeId = Customer.SupportRepId
JOIN Invoice On Customer.CustomerId = Invoice.CustomerId;
```
(8) Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
```
SELECT Customer.FirstName ||" "|| Customer.LastName As "Customer", Customer.Country, Employee.FirstName || " " || Employee.LastName As "Sales Agent", Invoice.Total 
FROM Employee
JOIN Customer On Employee.EmployeeId = Customer.SupportRepId
JOIN Invoice On Customer.CustomerId = Invoice.CustomerId;
```
(9) How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
```
SELECT * 
FROM Invoice
WHERE InvoiceDate LIKE "2009%" OR InvoiceDate LIKE "2011%";
```
```
SELECT SUM(Total) 
FROM Invoice
WHERE InvoiceDate LIKE "2009%";
```
```
SELECT SUM(Total)
FROM Invoice
WHERE InvoiceDate LIKE "2011%";
```
(10) Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
```
SELECT Count(InvoiceLineId)
FROM InvoiceLine
JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
WHERE Invoice.InvoiceId = 37;
```
(11) Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
```
SELECT Invoice.InvoiceId, Count(InvoiceLineId) AS "Line Items"
FROM Invoice
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId
GROUP BY Invoice.InvoiceId
```
(12) Provide a query that includes the track name with each invoice line item.
```
SELECT InvoiceLine.*, Track.Name AS "Track"
FROM InvoiceLine
JOIN Track ON InvoiceLine.TrackId = Track.TrackId;
```
(13) Provide a query that includes the purchased track name AND artist name with each invoice line item.
```
SELECT InvoiceLine.*, Artist.Name AS "Artist", Track.Name AS "Track"
FROM InvoiceLine
JOIN Track ON InvoiceLine.TrackId = Track.TrackId
JOIN Album ON Track.AlbumId = Album.ArtistId
JOIN Artist ON Album.ArtistId = Artist.ArtistId
GROUP BY InvoiceLine.InvoiceLineId
```
(14) Provide a query that shows the # of invoices per country. HINT: [GROUP BY](http://www.sqlite.org/lang_select.html#resultset)
```
SELECT BillingCountry, Count(InvoiceId) AS "Total Invoices"
FROM Invoice
GROUP BY BillingCountry
```
(15) Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resultant table.
```
SELECT Playlist.Name AS "Playlist", Count(Track.TrackId) AS "Total Tracks"
FROM Playlist
JOIN PlayListTrack ON Playlist.PlaylistId = PlaylistTrack.PlaylistId
JOIN Track ON PlaylistTrack.TrackId = Track.TrackId
GROUP BY "Playlist"
```
(16) Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
```

```
(17) Provide a query that shows all Invoices but includes the # of invoice line items.
```

```
(18) Provide a query that shows total sales made by each sales agent.
```

```
(19) Which sales agent made the most in sales in 2009?
```

```
(20) Which sales agent made the most in sales in 2010?
```

```
(21) Which sales agent made the most in sales over all?
```

```
(22) Provide a query that shows the # of customers assigned to each sales agent.
```

```
(23) Provide a query that shows the total sales per country. Which country's customers spent the most?
```

```
(24) Provide a query that shows the most purchased track of 2013.
```

```
(25) Provide a query that shows the top 5 most purchased tracks over all.
```

```
(26) Provide a query that shows the top 3 best selling artists.
```

```
(27) Provide a query that shows the most purchased Media Type.
```

```
