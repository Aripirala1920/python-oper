# python-oper
import requests

def get_weather(city):
    api_key = "your_api_key"
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}"
    response = requests.get(url)
    data = response.json()
    temperature = data['main']['temp']
    weather = data['weather'][0]['description']
    return temperature, weather

city = "London"
temperature, weather = get_weather(city)
print(f"Temperature: {temperature}")
print(f"Weather: {weather}")
