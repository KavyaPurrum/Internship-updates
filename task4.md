import requests

city = input("Enter city name: ")

url = f"https://wttr.in/{city}?format=j1"

response = requests.get(url)
data = response.json()

temp = data["current_condition"][0]["temp_C"]
humidity = data["current_condition"][0]["humidity"]
weather = data["current_condition"][0]["weatherDesc"][0]["value"]

print("\n🌍 Weather Report")
print("City:", city)
print("Temperature:", temp, "°C")
print("Humidity:", humidity, "%")
print("Condition:", weather)
