# SQL-Movies-1915-2023-cleaning

    SELECT TOP (1000) [column1]
      ,[Movie_Name]
      ,[Year_of_Release]
      ,[Run_Time_in_minutes]
      ,[Movie_Rating]
      ,[Votes]
      ,[MetaScore]
      ,[Gross]
      ,[Genre]
      ,[Certification]
      ,[Director]
      ,[Stars]
      ,[Description]
    FROM [Portfolio].[dbo].[data]


    select * from [data];

    select Movie_Rating, round (Movie_Rating, 1) from [data];


    select stars, len(stars)from [data];

    select Movie_Name, len(Movie_Name)from [data];

    select Movie_Name, len(Movie_Name)-len(replace(Movie_Name, ' ',''))+1 from [data];

    select genre, len(genre)-len (replace(replace(genre, ' ,',''),',',''))+1 from [data];

    select * from data;


    select Genre, len(Genre)from [data];



    SELECT PARSENAME(Replace(Genre, '[', ''),1) from data;

    select genre from data;   



     select genre, replace(replace(replace(replace(genre,'[',''),']',''),'''',''),',','') as final from data


    select genre, len(genre)-len (replace(replace(replace(replace(genre,'[',''),']',''),'''',''),',',''))+1 as final from data

    select Stars, replace(replace(replace(stars,'[',''),']',''),'''','') as final from data

  

  --Drop column1 and Description column
  alter table data drop column description;
  select * from data;
  
  -- Remove brackets and quotation on descriptions in Genre column

    select genre, replace(replace(replace(genre,'[',''),']',''),'''','') as GENRE from data;

--Update genre column with the corrected description

    update [data]
    set genre=replace(replace(replace(genre,'[',''),']',''),'''','')  from data;

    select * from [data];

  -- Remove brackets and quotation from directors column

    select director, replace(replace(replace(director,'[',''),']',''),'''','') as DIRECTOR from data;

--Update directors column with correct description

    update [data]
    set director=replace(replace(replace(director,'[',''),']',''),'''','') from data;

  --To get a count of stars from stars name in stars column

    select Stars, replace(replace(replace(stars,'[',''),']',''),'''','') as final from data

  --Then update stars column
    update [data]
    set stars= replace(replace(replace(stars,'[',''),']',''),'''','')  from data

  --Get count

    select stars, len(stars)-len (replace(replace(replace(replace(stars,'[',''),']',''),'''',''),',',''))+1 as count from data

  

  -- Remove null values in metascore and gross column

    delete from [data]
    where metascore is null or gross is null;

  --Round up value in Gross column

    select gross, round(gross,1) from data;
  
    update [data]
    set gross= round(gross,1) from data;


  -- Add rating to null values in certification column based on similar rated genre from genre column

    select distinct (genre),certification, count(genre) as occurence from [data]
    group by genre, certification;

    select genre, certification from data where certification is null;

  
    select certification, isnull(certification,'R') from [data]


    select genre,certification, isnull(certification,'R') from data WHERE genre 
    like 'Crime,  Drama,  Romance' or genre like 'Drama,  Romance'or genre 
    like 'Drama,  Thriller' or genre like 'Drama,  Fantasy,  Horror'
    or genre like 'Drama,  Mystery' or genre like 'Drama,  History,  Thriller'
    or genre like 'Drama  Sports,  Thriller' or genre like 'Comedy,  Drama,  Romance';

--Update certification column

    update [data]
    set certification= isnull(certification,'R') from data WHERE genre 
    like 'Crime,  Drama,  Romance' or genre like 'Drama,  Romance'or genre 
    like 'Drama,  Thriller' or genre like 'Drama,  Fantasy,  Horror'
    or genre like 'Drama,  Mystery' or genre like 'Drama,  History,  Thriller'
    or genre like 'Drama  Sports,  Thriller' or genre like 'Comedy,  Drama,  Romance';


    select genre, certification,isnull(certification,'PG-13')from [data]
    where genre like 'Animation,  Action,  Drama' or 
    genre like'Drama,  Sports,  Thriller' or genre like 'Comedy,  Drama'
    or genre like 'Comedy,  Music' or genre like 'Drama'
  
    update [data]
    set certification = isnull(certification,'PG-13')from [data]
    where genre like 'Animation,  Action,  Drama' or 
    genre like'Drama,  Sports,  Thriller' or genre like 'Comedy,  Drama'
    or genre like 'Comedy,  Music' or genre like 'Drama'

  --where genre like 'horror';

