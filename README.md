

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

#STEP2: Using intermediate files produced above to determine the number of dela$
while read -r line
do
grep 1 > GNV_ATL_delayedflights.tsv
done<$file3

while read -r line
do
grep 1 > GNV_CLT_delayedflights.tsv
done<$file4

while read -r line
do
grep 1 > GNV_MIA_delayedflights.tsv
done<$file5

file6=./GNV_ATL_delayedflights.tsv
file7=./GNV_CLT_delayedflights.tsv
file8=./GNV_MIA_delayedflights.tsv


wc -l $file6 >> results_table.tsv
wc -l $file7 >> results_table.tsv
wc -l $file8 >> results_table.tsv
