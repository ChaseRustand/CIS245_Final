# CIS245_Final
import requests

# function to request for data
def weather_data(query):
   # Enter your API key here
   api_key = "644528623dfc32e45d01ca0cd60d8f9c"
   # base_url variable to store url
   
   base_url = "http://api.openweathermap.org/data/2.5/weather?"
  
   complete_url = base_url + "appid=" + api_key + "&" + query

   # response object
   res=requests.get(complete_url);
   return res.json();

def testConn(query):
   # Enter your API key here
    api_key = "644528623dfc32e45d01ca0cd60d8f9c"
   # base_url variable to store url
   
    base_url = "http://api.openweathermap.org/data/2.5/weather?"
  
    complete_url = base_url + "appid=" + api_key + "&" + query

   # response object
    res=requests.get(complete_url);
    return res.status_code  

# function to display results
def display_results(weathers,city):
    #city

  # print("{}'s name: {}".format(city['weather']))
   print("{}'s temperature: {}°C ".format(city,weathers['main']['temp']))
   print("Wind speed: {} m/s".format(weathers['wind']['speed']))
   print("Description: {}".format(weathers['weather'][0]['description']))
   print("Weather: {}".format(weathers['weather'][0]['main']))


# main function
def main():

   check = 'yes'
   while check == 'yes':
    # Give city name
    city=input('Enter the city:')
    print()
    # try-except block
    try:
        query='q='+city;
        w_data=weather_data(query);
        display_results(w_data, city)
        conn = testConn(query)
        if conn == 200:
            print('Succesful Connection')
        else:
            print('Failed Connection')
        
        print()
        
        check=input('Would you like to check another city? Yes or No: ')

    except:
        print('City name not found')
    if(check == 'no'):
        print('Thank you! Exiting...')


if __name__=='__main__':
   main()
