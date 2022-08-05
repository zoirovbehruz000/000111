# 000111
Tavsiflar yo'q
from pytube import YouTube
from pywebio.input import *
from pywebio.output import *
from pywebio import start_server
from moviepy.editor import *


def app():
      url = input ("Vidio URL ni kiriting :")
      kengaytma = select("Kengaytmasini kiriting ",['mp4','3gpp','mp3'])
      toast("<<< Iltimos kuting >>>")
      if kengaytma == 'mp3':
            put_html("<h1>Afsuski mp3 formatda yuklashni iloji yo'q chunki u vidio formatida  </h1>")
            put_html("<h1>Ammo uni qayta ishlab mp3 formatiga o'girish mumkin uning uchun</h1>")
            put_html("<h1>Vidio sizning kompyuteringizga mp4 formatda o'rnataman</h1>")
            put_html("<h1>Siz esa uni nomini bu yerga kiritasiz</h1>")
            put_html("<h1>Va men uni mp3 ga o'giraman</h1>")
            put_button(['Boshlash'], onclick=ornat)
            
      try:
            put_html("<h1>Jarayon Boshlandi!!!</h1>")
            YouTube(url).streams.filter(file_extension=f'{kengaytma}').first().download()
            yt = YouTube(url)
            yt.streams
      except:
            toast("Iltimos URL ni to'g'ri kiriting")
      finally:
            toast ("Vidio yuklandi !")
            put_html("<h1>Vidio yuklandi !</h1>")


def ornat():
      url = input ("Vidio URL ni boshidan kiriting :")
      toast("Jarayon Boshlandi!!!")
      put_html("<h1>Jarayon Boshlandi!!!</h1>")
      try:
            YouTube(url).streams.filter(file_extension='mp4').first().download()
            yt = YouTube(url)
            yt.streams
      except:
            toast("Iltimos URL ni to'g'ri kiriting")
      finally:
            put_html("<h1>Vidio yuklandi !</h1>")
            toast ("Vidio yuklandi !")
            name=input("To'liq nomini kiriting",placeholder="U kompyuteringizda")
            toast("Jarayon Boshlandi!!!")
            mp4 = f"{name}.mp4"
            mp3 = f"{name}.mp3"
            Videoclip = VideoFileClip(mp4)
            audioclip = Videoclip.audio
            audioclip.write_audiofile(mp3)
            audioclip.close()
            Videoclip.close()
            toast ("Audio yuklandi !")

start_server(app, debug=True, port="8080")
