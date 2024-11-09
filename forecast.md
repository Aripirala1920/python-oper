import requests

def get_weather(city):
    api_key = "your_api_key"
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}"
    
    try:
        response = requests.get(url)
        response.raise_for_status()  # Check for HTTP errors
        data = response.json()
        
        temperature = data['main']['temp']
        humidity = data['main']['humidity']
        weather_description = data['weather'][0]['description']
        
        return temperature, humidity, weather_description
    except requests.exceptions.HTTPError as errh:
        return f"HTTP Error: {errh}"
    except requests.exceptions.ConnectionError as errc:
        return f"Error Connecting: {errc}"
    except requests.exceptions.Timeout as errt:
        return f"Timeout Error: {errt}"
    except requests.exceptions.RequestException as err:
        return f"Request Error: {err}"

def main():
    city = input("Enter the city name: ")
    weather = get_weather(city)
    
    if isinstance(weather, tuple):
        temperature, humidity, weather_description = weather
        print(f"Temperature: {temperature}K")
        print(f"Humidity: {humidity}%")
        print(f"Weather: {weather_description}")
    else:
        print(weather)

if __name__ == "__main__":
    main()
