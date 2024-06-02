# survey-data-response-project
python project on the years of experience vs the average salary of individuals.

import csv

with open('c:\zenath\Survey-Data.csv') as f:
    reader = csv.reader(f, delimiter=",")
    sample_data = list(reader)

column_names = sample_data[0]
survey_responses = sample_data[1:]

for row in survey_responses:
    row[0] = float(row[0])
    row[1] = row[1] == "TRUE" 
    row[2] = row[2] == "TRUE" 
    row[3] = row[3] == "TRUE" 
    row[4] = None if row[4] == "None" else row[4]
    row[5] = int(row[5])   
    
C_lang_count = 0
CPlusPlus_count = 0
Java_count = 0
for row in survey_responses:
    C_lang_count += 1 if row[1] == True else 0
    CPlusPlus_count += 1 if row[2] == True else 0
    Java_count += 1 if row[3] == True else 0
    
count = [C_lang_count,CPlusPlus_count,Java_count]
num_of_C_lang = f'Number of C Language users: {count[0]}'
num_of_CplusPlus = f'Number of C++ users:  {count[1]}'
num_of_Java= f'Number of Java users: {count[2]}'


coding_exp = []
compensation = []
for row in survey_responses:
    coding_exp.append(row[0])
    compensation.append(row[5])
#   
exp_min=f'Minimum experience:\n{min(coding_exp)} Years'
exp_max=f' Maximum experience:\n{max(coding_exp)} Years'
exp_average=f"Average experience:\n{round(sum(coding_exp)/len(coding_exp))} Years"
#
compn_min=f'Minimum compensation:\n${min(compensation)}'
compn_max=f'Maximum compensation:\n${max(compensation)}'
compn_average=f'Average compensation:\n${round(sum(compensation)/len(compensation),2)}'



by_exp=[0,0,0,0,0,0]
by_compn =[0,0,0,0,0,0]
years_and_compn =[['0-5 Years of experience',
            '5-10 Years of experience',
            '10-15 Years of experience',
            '15-20 Years of experience',
            '20-25 Years of experience',
            '+25 Years of experience'],
            ['0-50K','50K-100K','100K-150K',
             '150K-200K','200K-250K','+250K']]
for row in survey_responses:
    experience = row[0]
    compensated = row[5]
    by_exp[0]+=1 if 0< experience <=5 else 0
    by_exp[1]+=1 if 5< experience <=10 else 0
    by_exp[2]+=1 if 10< experience <=15 else 0
    by_exp[3]+=1 if 15< experience <=20 else 0
    by_exp[4]+=1 if 20< experience <=25 else 0
    by_exp[5]+=1 if experience > 25 else 0
    
    by_compn[0]+= 1 if 0 < compensated <= 50000 else 0
    by_compn[1]+= 1 if 50000 < compensated <= 100000 else 0
    by_compn[2]+= 1 if 100000 < compensated <= 150000 else 0
    by_compn[3]+= 1 if 150000 < compensated <= 200000 else 0
    by_compn[4]+= 1 if 200000 < compensated <= 250000 else 0
    by_compn[5]+= 1 if compensated>250000 else 0


for money in range(len(by_compn)):
    total_compn = 0
    num_ppl = 0
    for row in survey_responses:
        exp = row[0]
        compn = row[5]
        #e4 = 0000,e5 = 00000, so 5e4 = 50000 or 50K
        if money == 0 and 0<compn<=5e4 and 0<exp<=5:
            total_compn+=compn
            num_ppl+=1
        elif money == 1 and 5e4<compn<=1e5 and 5<exp<=10:
            total_compn+=compn
            num_ppl+=1
        elif money == 2  and 1e5<compn<=1.5e5 and 10<exp<=15:
            total_compn+=compn
            num_ppl+=1
        elif money == 3 and 1.5e5<compn<=2e5 and 15<exp<=20:
            total_compn+=compn
            num_ppl+=1
        elif money == 4 and 2e5<compn<=2.5e5 and 20<exp<=25:
            total_compn+=compn
            num_ppl+=1
        elif money == 5 and compn>2.5e5 and exp>25:
            total_compn+=compn
            num_ppl+=1
    average_compn = total_compn/num_ppl if num_ppl>0 else 0
    average_compn = round(average_compn,2)
    print(f"People with {years_and_compn[0][money]}\n Have an average salary of:{average_compn}\n")




total_compn=0
compn_and_exp =[0,0,0,0,0,0]

for row in survey_responses:
    exp = row[0]
    compn = row[5]
    compn_and_exp[0]+=1 if 0<exp<=5 and 0<compn<=50000 else 0 
    compn_and_exp[1]+=1 if 5<exp<=10 and 50000<compn<=100000 else 0
    compn_and_exp[2]+=1 if 10<exp<=15 and 100000<compn<=150000 else 0
    compn_and_exp[3]+=1 if 15<exp<=20 and 150000<compn<=200000 else 0
    compn_and_exp[4]+=1 if 20<exp<=25 and 200000<compn<=250000 else 0
    compn_and_exp[5]+=1 if exp>25 and compn>250000 else 0
    

#####################################################################################################
#Please find below output of above program
"""
runfile('C:/zenath/My-Survey-Project.py', wdir='C:/zenath')
People with 0-5 Years of experience
 Have an aveage salary of:9168.36

People with 5-10 Years of experience
 Have an average salary of:66306.6

People with 10-15 Years of experience
 Have an average salary of:116702.37

People with 15-20 Years of experience
 Have an average salary of:173858.15

People with 20-25 Years of experience
 Have an average salary of:223131.4

People with +25 Years of experience
 Have an average salary of:387638.07
""" 
##################################################################################################### 
Distribution of the experience categories:

-largest volume of users fall in to exp of 0-5 years with 68 to 71% of users falling into this category
-average compensation changes drastacically with 134% difference in average compensation between people with 0 - 5 years experience vs. people with 5 - 10 years experience with average compensation between people in 5 - 25 years difference being less 40% every 5 years.
-some extreme values are indivuals making 1 million dollars or more and equally indivuals making no money or less than 5000

######################################################################################################



    
