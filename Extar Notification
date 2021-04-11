import ezgmail 
from datetime import date
import datetime
import time
import pandas as pd 
from twilio.rest import Client
import os 



account_sid = #Hidden
auth_token = #Hidden
client = Client(account_sid, auth_token)

print('start Program') #pulling date from timestamp
today_date = date.today() #assigning today's date variable so it can be matched with message time stamp

# attributes of the first message 
#x.date provides the date, x.year provides year 

def checkemail():
    today_date = date.today()
    unreadThreads = ezgmail.unread()
    unread = ezgmail.search('Extar USA in stock')
 #searches email for subject EP9 that is unread which will be from extar ###!!! Search from extarusa 
    message = unread[0].messages[0] #the first unread message
    message_date = message.timestamp #pulling message timestamp
    message_date = message_date.date()
    if message_date == today_date:
        print('In Stock')
        print(message_date)
        print (today_date)
        send_text()

    else:
        print('Not in stock')
        print(datetime.datetime.now())
        time.sleep(60)
        checkemail()
        
def send_text():
   
    messages = client.messages.list(to='+')#phone number removed 
    black_list = []
    data = pd.read_csv('Documents/Phone List.csv', header=0)
    for record in messages:
            if record.from_ != '+' and record.from_ != '+' :#removed phone numbers for privacy 
                black_list.append(record.from_) 
                black_list = [y.strip('+') for y in black_list]      
                data = pd.read_csv('Documents/Phone List.csv', header=0)
                numbers_to_message= list(data.phone)
                numbers_to_message= [str(i) for i in numbers_to_message]
                Final_phone_list = [x for x in numbers_to_message if x not in black_list]
                Clean_list = [x for x in Final_phone_list if x != 'nan'] #removes 'nan' from list
    for number in Clean_list:
        message = client.messages.create(
        body='Message text sent to subscribers',
        from_='+phone number',#removed phone number
        to= number,)
        print(message.to)
        print(datetime.datetime.now())
        print("Extar's in stock")    
    print('done')
    time.sleep(43200)
    
 
checkemail()
