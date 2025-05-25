# Mutual Funds Data Scraper

This project scrapes mutual funds data from the website [Sarmaaya.pk](https://sarmaaya.pk/mutual-funds/) and saves it into a CSV file.

## 📦 Features

- Scrapes structured mutual fund data including serial number, fund name, NAV, YTD, etc.
- Automatically appends data to an existing CSV file or creates a new one.
- Cleans and sanitizes special characters (e.g., Unicode left-to-right markers).
- Error-handled for real-world scraping challenges (timeouts, element handling, etc.).

---

## 🧠 How It Works

### Libraries Used

- `requests` – to fetch HTML content.
- `BeautifulSoup` – to parse and extract HTML table data.
- `csv` – to write extracted data to a `.csv` file.
- `os` – to check if file already exists.

### Code Flow

```python
# 1. Check if CSV file exists
file_exists = os.path.exists(csv_file)

# 2. Make GET request and parse with BeautifulSoup
soup = BeautifulSoup(requests.get(url).content, "html.parser")

# 3. Locate the data table by ID
data_table = soup.find("table", {"id": "funds-table"})

# 4. Extract headers and data rows
headers = ["Serial No"] + [cell.text.strip() for cell in data_table.find("thead").find_all("th")]

# 5. Write to CSV file (append mode)
