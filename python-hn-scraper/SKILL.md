---
name: python-hn-scraper
description: Set up and run a Python-based Hacker News headline scraper. Use when the user needs to extract top news from HN or wants a template for Python web scraping in Termux.
---

# Python HN Scraper

This skill provides a fast path to setting up a BeautifulSoup-based scraper for Hacker News.

## Procedure

### 1. Setup Environment
Create a dedicated project directory:
```bash
mkdir -p ~/python-hn-scraper && cd ~/python-hn-scraper
```

### 2. Create Scraper Script
Write the following to `scraper.py`:
```python
import requests
from bs4 import BeautifulSoup
import json

def get_hn_headlines():
    url = "https://news.ycombinator.com/"
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    headlines = []
    for item in soup.find_all('span', class_='titleline'):
        link = item.find('a')
        headlines.append({"title": link.get_text(), "url": link.get('href')})
    return headlines[:10]

if __name__ == "__main__":
    results = get_hn_headlines()
    with open("headlines.json", "w") as f:
        json.dump(results, f, indent=2)
    print(f"✓ Saved {len(results)} headlines to headlines.json")
```

### 3. Install Dependencies
Always use `--break-system-packages` on this Android system if not using a venv:
```bash
echo -e "requests\nbeautifulsoup4" > requirements.txt
pip install -r requirements.txt --break-system-packages
```

### 4. Execute and Verify
Run the script from its own directory to ensure file paths are correct:
```bash
python scraper.py
cat headlines.json
```

## Pitfalls
- **Directory Scope:** Always `cd` into the project folder before running `python scraper.py`, otherwise `headlines.json` may be created in an unexpected location.
- **Dependencies:** Ensure `pip` is available and libraries are installed with the system-package flag.
