# Location-trakar

from geopy.geocoders import Nominatim
import phonenumbers
from phonenumbers import geocoder, carrier

def get_location_info(phone_number_str):
    try:
        # নম্বর বিশ্লেষণ
        phone_number = phonenumbers.parse(phone_number_str)
        
        # লোকেশন এবং সেবার নাম খুঁজে বের করা
        location = geocoder.description_for_number(phone_number, "en")
        service_provider = carrier.name_for_number(phone_number, "en")
        
        if location:
            # GeoPy ব্যবহার করে লোকেশন পাওয়া
            geolocator = Nominatim(user_agent="geoapiExercises")
            location_detail = geolocator.geocode(location)
            
            if location_detail:
                return {
                    "Location": location,
                    "Service Provider": service_provider,
                    "Latitude": location_detail.latitude,
                    "Longitude": location_detail.longitude
                }
            else:
                return {
                    "Location": location,
                    "Service Provider": service_provider,
                    "Latitude": "Not found",
                    "Longitude": "Not found"
                }
        else:
            return {
                "Location": "Not found",
                "Service Provider": service_provider,
                "Latitude": "Not found",
                "Longitude": "Not found"
            }
    except phonenumbers.NumberParseException as e:
        return {"Error": str(e)}

# নম্বর সেটআপ
phone_number_str = "+8801712345678"  # নম্বরের আগে দেশের কোড (+880 বাংলাদেশ)

# লোকেশন তথ্য সংগ্রহ
info = get_location_info(phone_number_str)

# ফলাফল প্রিন্ট করা
for key, value in info.items():
    print(f"{key}: {value}")





কিভাবে রান করব:
Python ইন্সটল করা থাকলে, উপরোক্ত লাইব্রেরিগুলি ইন্সটল করে নাও:

bash
Copy code
pip install geopy phonenumbers
কোডটি একটি Python ফাইলে সংরক্ষণ করো, যেমন location_tracker.py, এবং কমান্ড লাইনে রান করো:

bash
Copy code
python location_tracker.py
