  # code1
import os

import requests
  from bs4 import BeautifulSoup
  
  BASE_URL = "https://www.cas.org"
  LOG_DIR = "crawl_logs"
  
  # Create the log directory if it doesn't exist
  os.makedirs(LOG_DIR, exist_ok=True)
  
  def crawl_url(url):
      response = requests.get(url)
      if response.status_code == 200:
          soup = BeautifulSoup(response.text, 'html.parser')
  
          # Extract data from the website and adjust this part based on the actual HTML structure
          element = soup.find('div', class_='your-class-name')
  
          if element is not None:
              data = element.get_text()
  
              # Create a file with a name based on the URL
              filename = os.path.join(LOG_DIR, f"{url.replace('/', '_')}.txt")
              with open(filename, 'w') as file:
                  file.write(data)
              print(f"Data from {url} has been saved to {filename}")
          else:
              print(f"No data found for {url}")
  
  def main():
      crawl_url(BASE_URL)
  
  if __name__ == "__main__":
      main()
