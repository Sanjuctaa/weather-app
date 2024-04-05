# weather-app

from tkinter import *

from tkinter import messagebox

import requests 

def getweather():

    city= city_name.get()
    
    api='https://api.openweathermap.org/data/2.5/weather?q='+city+'&appid={API_ID}'
    
    data=requests.get(api).json()
    
    cond= data['weather'][0]['main']
    
    desc= data['weather'][0]['description']
    
    temp= int(data['main']['temp']-273.15)
    
    min_temp= int(data['main']['temp_min']-273.15)
    
    max_temp= int(data['main']['temp_max']-273.15)
    
    pressure= data['main']['pressure']
    
    humidity= data['main']['humidity']
    
    
    
    final_info= "Condition:"+cond+'\n'+"Description: "+desc+'\n'+"Temperature: "+str(temp)+chr(176)+"C"
    
    final_data="Max-temp: "+str(max_temp)+"\n"+"Min-temp: "+str(min_temp)+"\n"+"Pressure: "+str(pressure)+"\n"+"Humidity: "+str(humidity)
        
    label1.config(text= final_info)
    
    label2.config(text= final_data)


win= Tk()

win.title("App")

win.config(bg="#00B4DB")

win.geometry('500x650+200+100')



# label
name_label= Label(win, text="Weather App",font=("Times New roman",'30'), bg='dark blue', fg='white')

name_label.place(y=50,width=500,height=50)


city_name= StringVar()

my_entry=Entry(win,font=('Times New roman',18),textvariable= city_name)

my_entry.place(x=25,y=140,width=450,height=50)


but=Button(win,text='Done',font=('Times New roman',18),command= getweather)

but.place(x=200,y=210,width=100,height=40)


frame= Frame(win,bg='white')

frame.place(x=50,y=270,width=400,height=270 )

label3=Label(frame,justify=CENTER,text="Weather Details",font=('Times New roman',15), fg="white", bg="grey")

label3.pack(fill=BOTH, expand=True)

label1=Label(frame,justify=CENTER,font=('Times New roman',13))

label1.pack(fill=BOTH, expand=True)

label2=Label(frame,justify=CENTER,font=('Times New roman',11))

label2.pack(fill=BOTH, expand=True)


win.mainloop()
