# Data Description

---
The required data is as follows.

1. List of shelters in Shibuya Ward
Data on evacuation shelters in Shibuya Ward will be extracted from the open data on the Shibuya Ward website. You can download the csv file from this [URL](https://www.city.shibuya.tokyo.jp/kusei/tokei/opendata/index1.html).
2. geopy
The location information of Shibuya Ward is extracted from geopy.
3. [Foursquare API](https://developer.foursquare.com/)
This API will be used for accessing venues at or near the desired locations. It allows us to make 500 premium calls a day. Credentials for a developer account were used to obtain a client ID and client secret.
4. The number of registered residents
The number of registered residents in Shibuya Ward is obtained from [the website of the ward office](https://www.city.shibuya.tokyo.jp/kusei/tokei/jinko/jumin.html). It is used to estimate the number of people allowed to evacuate per evacuation facility.
