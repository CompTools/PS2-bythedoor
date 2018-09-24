# Question1:
#!/bin/bash
#After running this code, we then opened the final file with nano -c to get the answer for number 1.
#STEP1
file=./flights.May2017-Apr2018.csv
while read -r line;
do
cut -d ',' -f 3,7,13,16 > threecolumns.csv;
done<$file

#STEP2
file2=./threecolumns.csv;
while read -r line;
do
grep GNV  > filtered_columns.csv;
done<$file2

#STEP3
file3=./filtered_columns.csv;
while read -r line;
do
grep 1 > GNV_delayed_flights.csv;
done<$file3

# Question2:

#!/bin/bash


# STEP1, utilizing one of the intermediate files produced in problem 1 to generate column1 data values

#Find count of all lines with flights from GNV to ATL
file2=./filtered_columns.csv
while read -r line;
do
grep \"[G][N][V]\"\,\"[A][T][L]\"  > all_GNV_to_ATL_flights.csv;
done<$file2
file3=./all_GNV_to_ATL_flights.csv
wc -l $file3 > results_table.tsv

#Find count of all lines with flights from GNV to CLT
while read -r line;
do
grep \"[G][N][V]\"\,\"[C][L][T]\" > all_GNV_to_CLT_flights.csv
done<$file2
file4=./all_GNV_to_CLT_flights.csv
wc -l $file4 >> results_table.tsv

#Find count of all lines with flights from GNV to MIA
while read -r line;
do
grep \"[G][N][V]\"\,\"[M][I][A]\" > all_GNV_to_MIA_flights.csv
done<$file2
file5=./all_GNV_to_MIA_flights.csv
wc -l $file5 >> results_table.tsv

#STEP2: Using intermediate files produced above to determine the number of delayed flights from GNV into each of the cities of interest
#Find lines with delayed flights from GNV to ATL
while read -r line
do
grep 1 > GNV_ATL_delayedflights.tsv
done<$file3

#Find lines with delayed flights from GNV to CLT
while read -r line
do
grep 1 > GNV_CLT_delayedflights.tsv
done<$file4

#Find lines with delayed flights from GNV to MIA
while read -r line
do
grep 1 > GNV_MIA_delayedflights.tsv
done<$file5

#Create variables for the intermeidate files
file6=./GNV_ATL_delayedflights.tsv
file7=./GNV_CLT_delayedflights.tsv
file8=./GNV_MIA_delayedflights.tsv

#Find counts of delayed flights
wc -l $file6 >> results_table.tsv
wc -l $file7 >> results_table.tsv
wc -l $file8 >> results_table.tsv

#STEP3: Determine number of flights delayed due to weather into each location of interest from GNV
#Pull information from original file that includes weather delay info
file=./flights.May2017-Apr2018.csv
while read -r line;
do
cut -d ',' -f 3,7,25 > columns.csv;
done<$file

#Find all lines with flights from GNV to ATL
file1=./columns.csv
while read -r line
do
grep \"[G][N][V]\"\,\"[A][T][L]\" > forcolumn3ATL.csv
done<$file1

#Find all lines with flights from GNV to CLT
while read -r line
do
grep \"[G][N][V]\"\,\"[C][L][T]\" > forcolumn3CLT.csv
done<$file1

#Find all lines with flights from GNV to MIA
while read -r line
do
grep \"[G][N][V]\"\,\"[M][I][A]\" > forcolumn3MIA.csv
done<$file1

#Create variables for intermediate files
file9=./forcolumn3ATL.csv
file10=./forcolumn3CLT.csv
file11=./forcolumn3MIA.csv

#Find all lines with weather delay info from GNV to ATL
while read -r line
do
grep [1-9]\.[0-9]  > GNV_ATL_weatherdelays.csv
done<$file9

#Find all lines with weather delay info from GNV to CLT
while read -r line
do
grep [1-9]\.[0-9]  > GNV_CLT_weatherdelays.csv
done<$file10

#Find all lines with weather delay info from GNV to MIA
while read -r line
do
grep [1-9]\.[0-9]  > GNV_MIA_weatherdelays.csv
done<$file11

#Create variables for intermediate files
file12=./GNV_ATL_weatherdelays.csv
file13=./GNV_CLT_weatherdelays.csv
file14=./GNV_MIA_weatherdelays.csv

#Count the number of weather delays from GNV into each airport of interest
wc -l $file12 >> results_table.tsv
wc -l $file13 >> results_table.tsv
wc -l $file14 >> results_table.tsv

#Create variable for the initial results file
file15=results_table.tsv

#Convert initial results file (which comes out as a list with 9 rows) to a table with 3 columns
grep all $file15 > results_table2.tsv
paste results_table2.tsv  <(grep delayed $file15) > results_table3.tsv
paste results_table3.tsv <(grep weather $file15) > final_results_table.tsv

 # Question Number 3
 auc () {
               cut -d, -f3 flights.May2017-Apr2018.csv > airportcodes.csv
               #cuts the column containing origin airport codes from the file and puts it into a new file
               cut -d, -f7 flights.May2017-Apr2018.csv >> airportcodes.csv
               #cuts the column containing the destination airport codes from the file and appends it to the bottom of the file conatining the origin airport codes. This creates one file with one column listing all the airport codes.
               sort -u airportcodes.csv
               #sorts and creates a list of all the unique airport codes.
}




# Question Number 4

fla () {  cut -d, -f4,5,6 flights.May2017-Apr2018.csv | sort -u | grep .*[F][L].*;  }

