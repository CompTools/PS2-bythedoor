

#!/bin/bash


#STEP1, utilizing one of the intermediate files produced in problem 1 to generate column1
file2=./filtered_columns.csv
while read -r line;
do
grep \"[G][N][V]\"\,\"[A][T][L]\"  > all_GNV_to_ATL_flights.csv;
done<$file2

file3=./all_GNV_to_ATL_flights.csv
wc -l $file3 > results_table.tsv

while read -r line;
do
grep \"[G][N][V]\"\,\"[C][L][T]\" > all_GNV_to_CLT_flights.csv
done<$file2

file4=./all_GNV_to_CLT_flights.csv
wc -l $file4 >> results_table.tsv

while read -r line;
do
grep \"[G][N][V]\"\,\"[M][I][A]\" > all_GNV_to_MIA_flights.csv
done<$file2

file5=./all_GNV_to_MIA_flights.csv
wc -l $file5 >> results_table.tsv
