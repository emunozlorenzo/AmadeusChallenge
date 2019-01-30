# AmadeusChallenge
Data Science Challenge for the recruiting process at Amadeus (Master in Data Science KSchool)
## Instructions
The data is avalible at http://export.airconomy.com/candidates/

  - You should do all the work in a Python Notebook
  - Export the Notebook to a public notebook viewer
  - Required: Include all your code in GitHub
  - Please promptly update the repository with your ongoing work

## Exercises
1. __Count the number of lines in Python for each file__
2. __Top 10 arrival airports in the world in 2013 (using the bookings file)__
- Arrival airport is the column arr_port. It is the IATA code for the airport
- To get the total number of passengers for an airport, you can sum the column pax, grouping by arr_port. Note that there is negative pax. That corresponds to cancelations. So to get the total number of passengers that have actually booked, you should sum including the negatives (that will remove the canceled bookings).
- Print the top 10 arrival airports in the standard output, including the number of passengers.

- __Bonus point__: Get the name of the city or airport corresponding to that airport (programatically, we suggest to have a look at GeoBases in Github)
- __Bonus point__: Solve this problem using pandas (instead of any other approach)
3. __Plot the monthly number of searches for flights arriving at Málaga, Madrid or Barcelona__
- For the arriving airport, you can use the Destination column in the searches file. 
- Plot a curve for Málaga, another one for Madrid, and another one for Barcelona, in the same figure.

- __Bonus point__: Solving this problem using pandas (instead of any other approach)
4. __Match searches with bookings__
- For every search in the searches file, find out whether the search ended up in a booking or not (using the info in the bookings file). For instance, search and booking origin and destination should match. 
- For the bookings file, origin and destination are the columns dep_port and arr_port, respectively. 
- Generate a CSV file with the search data, and an additional field, containing 1 if the search ended up in a booking, and 0 otherwise.
5. __Write a Web Service__
- Wrap the output of the second exercise in a web service that returns the data in JSON format (instead of printing to the standard output).
- The web service should accept a parameter n>0. For the top 10 airports, n is 10. For the X top airports, n is
