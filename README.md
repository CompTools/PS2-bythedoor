#Question1:
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

#Question2:


