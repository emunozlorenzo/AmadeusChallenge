# AmadeusChallenge
Data Science Challenge for the recruiting process at Amadeus (Master in Data Science KSchool)
## Instructions
The data is avalible at http://export.airconomy.com/candidates/

  - You should do all the work in a Python Notebook
  - Export the Notebook to a public notebook viewer
  - Required: Include all your code in GitHub
  - Please promptly update the repository with your ongoing work

## Exercises
1. [__Count the number of lines in Python for each file__](https://github.com/emunozlorenzo/AmadeusChallenge/blob/master/ch_01.empty.ipynb)
2. [__Top 10 arrival airports in the world in 2013 (using the bookings file)__](https://github.com/emunozlorenzo/AmadeusChallenge/blob/master/ch_02.empty.ipynb)
  - Arrival airport is the column arr_port. It is the IATA code for the airport
  - To get the total number of passengers for an airport, you can sum the column pax, grouping by arr_port. Note that there is negative pax. That corresponds to cancelations. So to get the total number of passengers that have actually booked, you should sum including the negatives (that will remove the canceled bookings).
  - Print the top 10 arrival airports in the standard output, including the number of passengers.

  - __Bonus point__: Get the name of the city or airport corresponding to that airport (programatically, we suggest to have a look at GeoBases in Github)
  - __Bonus point__: Solve this problem using pandas (instead of any other approach)
3. [__Plot the monthly number of searches for flights arriving at Málaga, Madrid or Barcelona__](https://github.com/emunozlorenzo/AmadeusChallenge/blob/master/ch_03.empty.ipynb)
  - For the arriving airport, you can use the Destination column in the searches file. 
  - Plot a curve for Málaga, another one for Madrid, and another one for Barcelona, in the same figure.

  - __Bonus point__: Solving this problem using pandas (instead of any other approach)
4. [__Match searches with bookings__](https://github.com/emunozlorenzo/AmadeusChallenge/blob/master/ch_04.empty.ipynb)
  - For every search in the searches file, find out whether the search ended up in a booking or not (using the info in the bookings file). For instance, search and booking origin and destination should match. 
  - For the bookings file, origin and destination are the columns dep_port and arr_port, respectively. 
  - Generate a CSV file with the search data, and an additional field, containing 1 if the search ended up in a booking, and 0 otherwise.
5. [__Write a Web Service__](https://github.com/emunozlorenzo/AmadeusChallenge/blob/master/ch_05.empty.ipynb)
  - Wrap the output of the second exercise in a web service that returns the data in JSON format (instead of printing to the standard output).
  - The web service should accept a parameter n>0. For the top 10 airports, n is 10. For the X top airports, n is

## Tips

### How to manage big files in chunks?

```
\# Reading CSV with Chunksize (Original File has 10.000.000 of rows)

df = pd.read_csv ('bookings.csv.bz2', sep = '^', usecols = ['arr_port', 'pax', 'year'],chunksize = 1000000)

\# Creating DataFrame where we are going to save the results of these chunks

sum_chunks = pd.DataFrame()

\# Loop to open all the chunks and execute the commands

k=0
for chunk in df:
    k += 1
    filtered_chunk = chunk[chunk['year'] == 2013]
    filtered_chunk.drop ('year', axis =1, inplace=True)
    nulls = filtered_chunk['pax'].isnull().sum()
    print ("Chunk %d: size of chunk %d, Null Values: %s"% (k,len(chunk),nulls))
    filtered_chunk.dropna(inplace=True)
    arr_ports = filtered_chunk.groupby ('arr_port')
    chunk_result = arr_ports.sum()
    sum_chunks = sum_chunks.append(chunk_result)

\# Using the file made of chunks to get the result

top10_ports_2013 = sum_chunks.groupby(sum_chunks.index).pax.sum().sort_values(ascending = False).head(10).reset_index()

```
