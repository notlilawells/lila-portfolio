---
date: '2022-12-15T12:50:54.000Z'
title: Chicago Food Inspections
tagline: Database Design & Development
preview: Designing a relational database for Chicago Food Inspections
image: 'https://source.unsplash.com/TLD6iCOlyb0'
---

# Overview 

I've been working with relational databases for some time now, so I figured it was time to try creating a database myself (with an interactive Python application to match!)

When searching for suitable datasets to convert into database form, I stumbled across a dataset by the the City of Chicago. The dataset (originally in CSV format) contained information derived from inspections of restaurants and other food establishments in Chicago from January 1, 2010 to the present. Inspections were performed by staff from the Chicago Department of Public Health Protection Program using a standardized procedure. The results of the inspection are inputted into a dataset file, then reviewed and approved by a State of Illinois Licensed Environmental Health Practitioner (LEHP)

# Live Demo 

You can try out my project live by clicking [here](https://replit.com/@LilaWells/Food-Inspections-App). 

**Note** You may have to click "run" on the Replit project file a few times for the database to "wake up." It is currently hosted on Microsoft Azure (using a free account) so clicking the "run" button several times on the Replit file will help to reactive the database file (and get it ready to interact with you!). 

# The Dataset 

The uncleaned dataset had over 600,000 observations across 20+ variables. So, I downloaded the file in CSV format and cleaned it with Python (i.e., removing duplicates and null values as well as outliers). I then divided the dataset into seven CSV files, and used Microsoft Azure's Import Wizard commands to refine and upload the CSV files to the cloud into a new database (which I very creatively called Food Food-Inspections

Each cleaned CSV file represented a future table in the database. When using Azure's Import Wizard commands, I specified several Foreign and Primary key constraints within each table (forming relationships between them).

# Entity Relationship Diagram

See the entity relationship diagram I created for the Food Inspections database below. You will see that, within the database itself, most tables have a one-to-many relationship with those adjascent to them.

![project04 drawio](https://user-images.githubusercontent.com/101524157/214749972-0bb15ced-fde3-4269-9d1a-c253ab54c0d4.png)

# The Commands

The commands I implemented were labeled 0 through 9. They are as follows:

**Command 0**: Outputs information on the database itself (i.e., how many stores and inspections, where the data comes from, where you can learn more about the data source).

**Command 1**: Outputs the number of inspections and the number of food establishments in the database.

**Command 2**: Outputs the percent of inspections in the database by inspection result.

**Command 3**: Here, you input a store type (ex. Restaurant, Grocery Store, or Daycare) and the program outputs the store ID, name, zip code and number of inspections for stores in that type.

**Command 4**: Here, you input a store type (ex. Restaurant, Grocery Store, or Daycare) and the program outputs the store ID, name, zip code, and inspection results for stores in that type that failed inspection.

**Command 5**: Here, you input a store ID and the program outputs information on that store and its inspections.

**Command 6**: Here, you input a Chicago zip code, and the program outputs information on stores that failed inspection in that zip code.

**Command 7**: Here, you input a Chicago zip code, and the program outputs information on stores that passed inspection in that zip code.

**Command 8**: Here, you input a Chicago zip code, and the program outputs store types in that zip code (i.e. restaurants, grocery stores, hospitals, daycares) and what percentage of store types in that zip code passed inspection.

**Command 9**: Here, you input a store ID and the program outputs what percent of that stores inspections that store passed, failed, passed with conditions, etc.


# A bit about the code

Below, I have included an explanation of my coding procedure for a few of the commands employed in this project (with code examples). 

All code for this project can be accessed in on GitHub by clicking [here](https://github.com/notlilawells/Food-Inspections-Database).

### Command 1
In the first command, I used a SQL SELECT statement to aggregate the number of movies and ratings in the database.

```python
# Placed within a larger while loop 
if cmd == "1": 
    sql1_pt1 = """
               SELECT COUNT(Movie_ID) 
               FROM Movies;
               """
    row = datatier.select_one_row(dbConn, sql1_pt1, [])
    print("# of movies", ":", f"{row[0]:,}")
    sql1_pt2 = """
           SELECT COUNT(Rating) 
             FROM Ratings
          """
    row = datatier.select_one_row(dbConn, sql1_pt2, [])
    print("# of reviews", ":", f"{row[0]:,}")
```

### Command 2
In the second command, I added an input statement (called name here) to later input into the SQL SELECT statement. This allowed me to extract only the movie IDs and titles for movies that had similar names to our input. I added an additional if/else statement here to allow for paging (i.e., when there are more than 20 results to the query). That way, the user has the option to display more options if they so choose.

```python
# Placed within a larger while loop 
elif cmd == "2":
    name = input("Enter movie name (e.g. '%matrix%'): ")
    sql2 = """
           SELECT Movie_ID, Title, STRFTIME('%Y', Release_Date) 
           FROM Movies 
           WHERE Title LIKE ?
           ORDER BY Movie_ID ASC;
           """
    dbCursor.execute(sql2, [name])
    rows = dbCursor.fetchall()

    if len(rows) == 0:
      print("no movie found")
    elif len(rows) <= 20:
      for row in rows:
        print(row[0], ":", row[1], ":", row[2])
    else:
      more = "this can be anything but no"
      i = 0
      while more != "no" and more != "n":
        end = i + 20
        if end > len(rows):
          end = len(rows)
          for row in rows[i:end]:
            print(row[0], ":", row[1], ":", row[2])
          print()
          more = "no"
        else:
          for row in rows[i:end]:
            print(row[0], ":", row[1], ":", row[2])
          print()
          more = input("Display more? [yes/no] ")
          i = i + 20
```

### Command 3
In the third command I followed a similar process. This time, I broke up the SQL commands into five parts (to fetch appropriate information from each table).

```python
# Placed within a larger while loop
 elif cmd == "3":
    id = input("Enter movie id: ")
    sql3_pt1 = """
              SELECT Title, Release_Date, Runtime, Original_Language, Budget, Revenue
              FROM Movies
              WHERE Movie_ID = ?;
              """
    sql3_pt2 = """
              SELECT COUNT(Rating), AVG(Rating)
              FROM Ratings
              WHERE Movie_ID = ?;
              """
    sql3_pt3 = """
              SELECT Genre_Name
              FROM Genres
              INNER JOIN Movie_Genres
                 ON Genres.Genre_ID = Movie_Genres.Genre_ID
              WHERE Movie_ID = ?
              ORDER BY Genre_Name ASC;
              """
    sql3_pt4 = """
              SELECT Company_Name
              FROM Companies
              INNER JOIN Movie_Production_Companies
                 ON Companies.Company_ID = Movie_Production_Companies.Company_ID
              WHERE Movie_ID = ?
              ORDER BY Company_Name ASC;
              """
    sql3_pt5 = """
              SELECT Tagline
              FROM Movie_Taglines
              WHERE Movie_ID = ?;
              """
    dbCursor.execute(sql3_pt1, [id])
    rows_pt1 = dbCursor.fetchall()

    dbCursor.execute(sql3_pt2, [id])
    rows_pt2 = dbCursor.fetchall()

    dbCursor.execute(sql3_pt3, [id])
    rows_pt3 = dbCursor.fetchall()

    dbCursor.execute(sql3_pt4, [id])
    rows_pt4 = dbCursor.fetchall()

    dbCursor.execute(sql3_pt5, [id])
    rows_pt5 = dbCursor.fetchall()

    if len(rows_pt1) == 0:
      print("no movie found")
    else:
      for row in rows_pt1:
        print(row[0])
        print("Release date", ":", row[1].split(" ")[0])
        print("Runtime", ":", row[2], "mins")
        print("Orig language", ":", row[3])
        print("Budget", ":", f"${row[4]:,}", "USD")
        print("Revenue", ":", f"${row[5]:,}", "USD")

      for row in rows_pt2:
        print("Num reviews", ":", row[0])
        if row[0] != 0:
          print("Avg rating", ":", f"{row[1]:.2f}", "out of 0..10")
        else:
          print("Avg rating", ":", "0.00", "out of 0..10")

      print("Genres")
      for row in rows_pt3:
        print("  ", row[0])

      print("Production companies")
      for row in rows_pt4:
        print("  ", row[0])

      if rows_pt5:
        print("Tagline:", rows_pt5[0][0])
      else:
        print("Tagline:")
```

### Command 4
In the fourth command, I used two input statements: one for N (the number of movies outputted) and one for min (the minimum number of reviews for the outputted movies). This allowed me to select for two conditions within the SQL statement.

```python
# Placed within a larger while loop
elif cmd == "4":
    N = input("N? ")
    N = int(N)
    if N < 1:  # invalid input
      print("Invalid value for N (must be positive)")
    else:
      min_reviews = int(input("min number of reviews? "))
      if min_reviews < 1:
        print("Invalid value for min (must be positive)")
      else:
        sql4 = """
              SELECT Movies.Movie_ID, AVG(Rating), Title
              FROM Movies
              INNER JOIN Ratings
                 ON Movies.Movie_ID = Ratings.Movie_ID
              GROUP BY Movies.Movie_ID
                HAVING COUNT(Rating) >= ?
              ORDER BY AVG(Rating) DESC, Title ASC;
              """
        dbCursor.execute(sql4, [min_reviews])
        rows = dbCursor.fetchall()

        for i in range(len(rows)):
          if i == N:
            break
          row = rows[i]
          print(row[0], ":", f"{row[1]:.2f}", ":", row[2])
```

### Command 5
In the fifth command, I followed a similar process to Command 2 (i.e., I created an if/else statement to allow for paging if need be).

```python
# Placed within a larger while loop
elif cmd == "5":
    genre = input("Enter genre (e.g. Action, Comedy, or Drama): ")

    sql5 = """
          SELECT Movies.Movie_ID, Title
            FROM Movies
           INNER JOIN Movie_Genres
              ON Movies.Movie_ID = Movie_Genres.Movie_ID
           INNER JOIN Genres
              ON Movie_Genres.Genre_ID = Genres.Genre_ID
           WHERE Genre_Name LIKE ?
           ORDER BY Movies.Movie_ID ASC;
          """
    dbCursor.execute(sql5, [genre])
    rows = dbCursor.fetchall()

    if len(rows) == 0:
      print("no movies found")
    elif len(rows) <= 20:
      for row in rows:
        print(row[0], ":", row[1])
    else:
      more = "this can be anything but no"
      i = 0
      while more != "no" and more != "n":
        end = i + 20
        if end > len(rows):
          end = len(rows)
          for row in rows[i:end]:
            print(row[0], ":", row[1])
          print()
          more = "no"
        else:
          for row in rows[i:end]:
            print(row[0], ":", row[1])
          print()
          more = input("Display more? [yes/no] ")
          i = i + 20
```

### Command 6
In the sixth command, I used a SQL INSERT command to dynamically change the database: allowing users to input new ratings into a movie by its id.

```python
# Placed within a larger while loop
elif cmd == "6":
    enter_id = int(input("Enter movie id: "))
    enter_rating = input("Enter rating (0..10): ")

    sql6 = """
          INSERT INTO Ratings(Movie_ID, Rating) Values(?, ?);
          """

    rows = datatier.perform_action(dbConn, sql6, [enter_id, enter_rating])

    if rows == -1:
      print("failed to add review")
    else:
      print("review successfully added")
```