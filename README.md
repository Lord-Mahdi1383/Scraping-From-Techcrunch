# Overview
A Python-based web scraping tool that extracts news articles from TechCrunch across multiple categories. This script uses Selenium to navigate through paginated content and collects article data in a structured format.  

# Features
  - Multi-Category Support: Scrapes articles from 5 TechCrunch categories:  
    Artificial Intelligence, Meta, Gaming, Apple and Space  
  - Pagination Handling: Automatically navigates through multiple pages (up to 10 pages per category)  
  - Duplicate Prevention: Uses a processed links set to avoid collecting duplicate articles  
  - Structured Data Export: Saves data in both CSV and JSON formats with proper formatting  

# How It Works?
**Step 1: Setup**    
  - Initialize headless Chrome browser with anti-detection settings  
  - Create category URL dictionary for targeted scraping

**Step 2: Category Processing**
  - Iterate through each category with pagination support
    - ```python
        page_url = f"{url.rstrip('/')}/page/{current_page}/" 
  - Navigate through multiple pages (up to 10 per category)  
  - Scroll to page bottom and wait for content loading
    - ```python
      driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
      time.sleep(2)   

**Step 3: Article Extraction**  
  - Identify article containers using multiple CSS selectors
  - Extract from each article: Title, URL, Date, and Image URL
      - ```python
        # Title and Title URL
        title_elem = container.find_element(By.CSS_SELECTOR, '.loop-card__title-link')
        title = title_elem.text.strip()
        link = title_elem.get_attribute('href')
      - ```python
        # Date
        date_elem = container.find_element(By.CSS_SELECTOR,  'time.loop-card__meta-item.loop-card__time.wp-block-tc23-post-time-ago')
        date = date_elem.get_attribute('datetime') or date_elem.text.strip()
      - ``` python
        # Image URL
        img_elem = container.find_element(By.CSS_SELECTOR, 'img.wp-post-image')
        image_url = img_elem.get_attribute('src') or img_elem.get_attribute('data-src')```
  - Implement duplicate prevention using link tracking  

**Step 4: Data Management**  
  - Structure extracted data into consistent format  
  - Accumulate articles by category (`category_articles`)  
  - Consolidate all categories into master collection (`all_articles`)  

**Step 5: Export & Cleanup**  
  - Convert data to pandas DataFrame  
  - Export to CSV and JSON formats with proper encoding  
  - Close browser driver to free resources

# Setup
### Clone The Repository
``` bash
git clone https://github.com/Lord-Mahdi1383/Scraping-From-Techcruch.git
cd Scraping-From-Techcrunc
```

### Install Requirements
``` bash
pip install -r Requirements.txt
```






