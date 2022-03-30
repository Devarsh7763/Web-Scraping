# Web-Scraping
#to Scrape the data and save the data in JSON format
# we need to import some library 
# here i used "Bs4" and for requesting the url i use "request" module
# to store some wher i used the module name Json
import requests
from bs4 import BeautifulSoup
import pandas as pd
import csv
import json
url="https://www.javatpoint.com/dbms-mcq"

res=requests.get(url).content
soup=BeautifulSoup(res,'html.parser')
#print(soup)
questions=soup.find_all('p',class_="pq")
answers=soup.find_all('div',class_="testanswer")
#print(title)
#print(answer)
mcq=[]
mcq_qu=[]
mcq_ans=[]

c=1
for question,answer in zip(questions,answers):
    #print(c,question)
    #print(answer)
    mcq_qu.append(question.text)
    mcq_ans.append(answer.text)
    c=c+1


#print(mcq_qu,sep="\n")
#print(mcq_ans,sep="\n")

#to save into a csv we need to put in a data frame
data={'question':mcq_qu,'answer':mcq_ans}

dev=pd.DataFrame(data)
print(dev.head())
#df.to_csv('mcq.csv',index=False)
# here i used seporator as \n ,while scraing the data was normal ,while i was saw in Json file ,it showed like hell i didn't that 
# so i used sep="\n"
dev.to_csv(r'E:\devarsh\ask_question.json',sep="\n")
