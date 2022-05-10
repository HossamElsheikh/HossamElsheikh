from tkinter import *
from tkinter import ttk
import speech_recognition as sr
from gtts import gTTS
import pygame.mixer
import time
pygame.mixer.init()
rec = sr.Recognizer()

def listen_user():
  with sr.Microphone() as source:
    print('Mr Robot Is Listening.....')
    audio = rec.listen(source, phrase_time_limit=3)
  try:
    text = rec.recognize_google(audio, language='en-US')
    print(text)
    time.sleep(0.5)
    return text 
  except:
    print("Sorry , I had a problem ")
    return 0

def talk(text , file):
  try:
    tts = gTTS(text= text , lang= "en")
    filename = "%s.mp3"%file
    tts.save(filename)
    time.sleep(1)
    pygame.mixer.music.load(filename)
    pygame.mixer.music.play()
    time.sleep(2)
  except:
    print('Error')

def conatct():
  text_returnd = listen_user()
  if "hello" in text_returnd:
    talk("Hello welcome to Mr Robot what is your name","b")
    time.sleep(0.5)
    phrase = listen_user()
    if phrase:
      name = phrase.split()[-1]
    else: name = "Hossam"
    talk(f"Your name is {name}","c")
  time.sleep(0.5)
  lisa = listen_user()
  if "how old are you" in lisa:
    talk("my age is month","g")
  else:
    print("I Dont know")
    time.sleep(1)
    



root = Tk()
root.title("Mr Robot")
root.geometry("522x553")
root.resizable(False , False)

rbt =PhotoImage(file = "pngegg.png")
Label(root , image= rbt).place(x=0 , y=0)


ttk.Button(root , text = "Start" , command=lambda:conatct() ).grid(column= 0 , row= 0 , padx= 10 , pady= 10 ,ipadx= 1 , ipady= 10)

root.mainloop()
