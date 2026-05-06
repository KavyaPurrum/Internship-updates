import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser

engine = pyttsx3.init()

def speak(text):
    print("Assistant:", text)
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        audio = r.listen(source)

    try:
        command = r.recognize_google(audio)
        print("You:", command)
        return command.lower()
    except:
        return ""

def reply(command):
    
    if "hello" in command or "hi" in command:
        return "Hello! How are you?"

    elif "how are you" in command:
        return "I am fine. How can I help you?"

    elif "your name" in command:
        return "I am your simple assistant"

    elif "time" in command:
        return "Time is " + datetime.datetime.now().strftime("%H:%M")

    elif "date" in command:
        return "Today's date is " + str(datetime.date.today())

    elif "who made you" in command:
        return "I was created using Python"

    elif "search" in command:
        speak("What should I search?")
        query = listen()
        webbrowser.open("https://www.google.com/search?q=" + query)
        return "Here are the results"

    elif "bye" in command or "stop" in command:
        return "bye"

    else:
        return "Sorry, I don't understand"

speak("Hello! I am your assistant")

while True:
    command = listen()
    if command == "":
        continue

    response = reply(command)

    if response == "bye":
        speak("Goodbye!")
        break
    else:
        speak(response)
