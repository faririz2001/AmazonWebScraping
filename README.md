# Project Title: Amazon Price Tracker  

## Description  
A Python-based web scraper that monitors the price of an Amazon product and stores the data in a CSV file. The script runs daily and logs the price along with the date to help users track price fluctuations.  

## Installation Instructions  
1. **Clone the repository**  
   ```sh
   git clone https://github.com/yourusername/amazon-price-tracker.git
   cd amazon-price-tracker

2. **Install dependencies**  
 ```sh
pip install -r requirements.txt

 ```

## The script requires:

* beautifulsoup4
* requests
* pandas

3. **Run the script**  
 ```sh
python price_tracker.py

 ```


## Usage

* Modify the `URL` variable inside `price_tracker.py` with the link to your desired Amazon product.
* The script runs once every 24 hours and appends the latest price data to `AmazonWebScraperDatabase.csv`.
* The collected data can be used for price trend analysis.


### Example Code
 ```python
import requests
from bs4 import BeautifulSoup
import datetime
import csv
import time

def check_price():
    URL = 'https://www.amazon.com/example-product/dp/B07FNW9FGJ/'
    headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"}
    
    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.content, "html.parser")

    title = soup.find(id='productTitle').get_text().strip()
    price_tag = soup.find('span', {'class': 'a-price-whole'})
    price = price_tag.get_text().strip() if price_tag else "N/A"
    
    today = datetime.date.today()
    data = [title, price, today]

    with open('AmazonWebScraperDatabase.csv', 'a+', newline='', encoding='UTF8') as f:
        writer = csv.writer(f)
        writer.writerow(data)
    
    print(f"Data saved: {title} - {price} on {today}")

while True:
    check_price()
    time.sleep(86400)

 ```

## Contribution Guidelines

* Fork the repository and create a new branch for your changes.
* Submit a pull request with a clear description of your modifications.
* Ensure code follows best practices and is tested before submission.


## License

This project is licensed under the MIT License.
