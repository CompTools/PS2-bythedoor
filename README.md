

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


#STEP3:

file=./flights.May2017-Apr2018.csv
while read -r line;
do
cut -d ',' -f 3,7,25 > columns.csv;
done<$file

file1=./columns.csv
while read -r line
do
grep \"[G][N][V]\"\,\"[A][T][L]\" > forcolumn3ATL.csv
done<$file1

while read -r line
do
grep \"[G][N][V]\"\,\"[C][L][T]\" > forcolumn3CLT.csv
done<$file1

while read -r line
do
grep \"[G][N][V]\"\,\"[M][I][A]\" > forcolumn3MIA.csv

file1=./columns.csv
while read -r line
do
grep \"[G][N][V]\"\,\"[A][T][L]\" > forcolumn3ATL.csv
done<$file1

while read -r line
do
grep \"[G][N][V]\"\,\"[C][L][T]\" > forcolumn3CLT.csv
done<$file1

while read -r line
do
grep \"[G][N][V]\"\,\"[M][I][A]\" > forcolumn3MIA.csv
done<$file1

file9=./forcolumn3ATL.csv
file10=./forcolumn3CLT.csv
file11=./forcolumn3MIA.csv

while read -r line
do
grep [1-9]\.[0-9]  > GNV_ATL_weatherdelays.csv
done<$file9

while read -r line
do
grep [1-9]\.[0-9]  > GNV_CLT_weatherdelays.csv
done<$file10

while read -r line

file9=./forcolumn3ATL.csv
file10=./forcolumn3CLT.csv
file11=./forcolumn3MIA.csv

while read -r line
do
grep [1-9]\.[0-9]  > GNV_ATL_weatherdelays.csv
done<$file9

while read -r line
do
grep [1-9]\.[0-9]  > GNV_CLT_weatherdelays.csv
done<$file10

while read -r line
do
grep [1-9]\.[0-9]  > GNV_MIA_weatherdelays.csv
done<$file11

file12=./GNV_ATL_weatherdelays.csv
file13=./GNV_CLT_weatherdelays.csv
file14=./GNV_MIA_weatherdelays.csv

wc -l $file12 >> results_table.tsv
wc -l $file13 >> results_table.tsv
wc -l $file14 >> results_table.tsv

file15=results_table.tsv

