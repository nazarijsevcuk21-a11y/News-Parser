# News-Parser
A project to demonstrate skills
# News Parser

A powerful web scraping tool for collecting and analyzing news from various websites with keyword filtering and export capabilities.

## Features

### Web Scraping
- Collect news from popular sites (Hacker News, BBC News)
- Universal parser for any news website
- Automatic page structure detection
- Support for multiple sources simultaneously

### Data Filtering
- Filter by keywords
- Search in titles and descriptions
- Case-insensitive matching
- Multiple keyword support

### Export Formats
- CSV - for analysis in Excel/Google Sheets
- JSON - for integration with other applications
- HTML - beautiful web report for viewing

### Data Analysis
- Statistics by source
- Statistics by category
- Total article count
- Last update tracking

## Technologies

- Python 3.8 or higher
- requests - HTTP client for web requests
- BeautifulSoup4 - HTML parsing
- lxml - fast parser
- Regular Expressions - pattern matching

## Installation

```bash
git clone https://github.com/yourusername/news-parser.git
cd news-parser
pip install -r requirements.txt
```

## Quick Start

### Basic Usage

```bash
python news_parser.py
```

The script will:
1. Collect news from Hacker News
2. Collect news from BBC Technology
3. Generate reports in the `output/` folder

### Run Examples

```bash
python examples.py
```

This will demonstrate 6 different usage scenarios.

## Usage as Library

### Basic Example

```python
from news_parser import NewsParser

# Create parser
parser = NewsParser()

# Collect news from Hacker News
articles = parser.parse_hacker_news(max_articles=20)
parser.add_articles(articles)

# Export to CSV
parser.export_to_csv("news.csv")
```

### With Filtering

```python
from news_parser import NewsParser

parser = NewsParser()

# Collect news
articles = parser.parse_hacker_news(max_articles=30)
parser.add_articles(articles)

# Filter by keywords
keywords = ["AI", "Python", "machine learning"]
filtered = parser.filter_by_keywords(keywords)

# Export filtered results
parser.export_to_csv("ai_news.csv", filtered)
parser.export_to_json("ai_news.json", filtered)
```

### Multiple Sources

```python
from news_parser import NewsParser

parser = NewsParser()

# Hacker News
hn_articles = parser.parse_hacker_news(max_articles=20)
parser.add_articles(hn_articles)

# BBC Technology
bbc_articles = parser.parse_bbc_news(category="technology", max_articles=15)
parser.add_articles(bbc_articles)

# BBC Business
business_articles = parser.parse_bbc_news(category="business", max_articles=10)
parser.add_articles(business_articles)

# Export all
parser.export_to_html("all_news.html")

# Get statistics
stats = parser.get_statistics()
print(f"Total: {stats['total']} articles")
print(f"Sources: {stats['sources']}")
```

## API Reference

### NewsParser Class

#### __init__(output_dir="output")
Initialize parser with specified output directory.

#### parse_hacker_news(max_articles=30)
Parse news from Hacker News.

**Parameters:**
- max_articles (int) - maximum number of articles

**Returns:** List[NewsArticle]

#### parse_bbc_news(category="technology", max_articles=20)
Parse news from BBC News.

**Parameters:**
- category (str) - news category (technology, business, science)
- max_articles (int) - maximum number of articles

**Returns:** List[NewsArticle]

#### parse_generic_news(url, max_articles=20)
Universal parser for any news website.

**Parameters:**
- url (str) - website URL
- max_articles (int) - maximum number of articles

**Returns:** List[NewsArticle]

#### filter_by_keywords(keywords)
Filter articles by keywords.

**Parameters:**
- keywords (List[str]) - list of keywords

**Returns:** List[NewsArticle]

#### export_to_csv(filename, articles=None)
Export articles to CSV file.

#### export_to_json(filename, articles=None)
Export articles to JSON file.

#### export_to_html(filename, articles=None)
Export articles to HTML file.

#### get_statistics()
Get statistics for collected articles.

**Returns:** Dict with keys: total, sources, categories

### NewsArticle Class

Represents a news article.

**Attributes:**
- title (str) - article title
- url (str) - article URL
- description (str) - article description
- date (str) - publication date
- category (str) - article category
- source (str) - news source

**Methods:**
- to_dict() - convert to dictionary
- matches_keywords(keywords) - check for keywords

## Examples

### Example 1: Collect and Export

```python
parser = NewsParser()

# Collect news
articles = parser.parse_hacker_news(max_articles=25)
parser.add_articles(articles)

# Export to various formats
parser.export_to_csv("hacker_news.csv")
parser.export_to_json("hacker_news.json")
parser.export_to_html("hacker_news.html")
```

### Example 2: Topic Filtering

```python
parser = NewsParser()

# Collect from BBC
tech_news = parser.parse_bbc_news("technology", max_articles=30)
parser.add_articles(tech_news)

# Filter for AI topics
ai_keywords = ["artificial intelligence", "AI", "machine learning", "neural"]
ai_news = parser.filter_by_keywords(ai_keywords)

print(f"Found {len(ai_news)} articles about AI")
parser.export_to_csv("ai_articles.csv", ai_news)
```

### Example 3: Topic Monitoring

```python
parser = NewsParser()

# Collect from various sources
parser.add_articles(parser.parse_hacker_news(max_articles=30))
parser.add_articles(parser.parse_bbc_news("technology", max_articles=20))

# Search for specific topics
python_news = parser.filter_by_keywords(["Python", "Django", "Flask"])
security_news = parser.filter_by_keywords(["security", "vulnerability", "hack"])

# Separate reports
parser.export_to_csv("python_news.csv", python_news)
parser.export_to_csv("security_news.csv", security_news)
```

### Example 4: Daily Digest

```python
from datetime import datetime

parser = NewsParser()

# Collect news from all sources
parser.add_articles(parser.parse_hacker_news(max_articles=20))
parser.add_articles(parser.parse_bbc_news("technology", max_articles=15))
parser.add_articles(parser.parse_bbc_news("business", max_articles=10))

# Create digest
date_str = datetime.now().strftime("%Y-%m-%d")
parser.export_to_html(f"daily_digest_{date_str}.html")
parser.export_to_json(f"daily_digest_{date_str}.json")

print(f"Digest for {date_str} created")
```

## Project Structure

```
news-parser/
├── news_parser.py          # Main module
├── examples.py             # Usage examples
├── requirements.txt        # Dependencies
├── README.md              # Documentation
├── QUICKSTART.md          # Quick start guide
├── SKILLS.md              # Technologies showcase
└── output/                # Output files (auto-created)
    ├── news.csv
    ├── news.json
    └── news.html
```

## Use Cases

### Industry News Monitoring

Monitor news in your industry on a daily basis:

```python
# Daily Python news collection
parser = NewsParser()
articles = parser.parse_hacker_news(max_articles=50)
parser.add_articles(articles)

python_news = parser.filter_by_keywords(["Python", "Django", "FastAPI"])
parser.export_to_csv(f"python_news_{datetime.now().date()}.csv", python_news)
```

### Competitive Analysis

Monitor news about competitors:

```python
# Monitor competitor news
competitors = ["OpenAI", "Google AI", "Microsoft AI"]
articles = parser.parse_bbc_news("technology", max_articles=50)
parser.add_articles(articles)

for company in competitors:
    company_news = parser.filter_by_keywords([company])
    parser.export_to_csv(f"{company}_news.csv", company_news)
```

### Trend Research

Collect news on specific topics:

```python
# Collect news by topics
topics = {
    "AI": ["artificial intelligence", "machine learning", "neural network"],
    "Crypto": ["bitcoin", "cryptocurrency", "blockchain"],
    "Climate": ["climate change", "global warming", "renewable energy"]
}

parser = NewsParser()
parser.add_articles(parser.parse_hacker_news(max_articles=100))

for topic_name, keywords in topics.items():
    topic_news = parser.filter_by_keywords(keywords)
    print(f"{topic_name}: {len(topic_news)} articles")
    parser.export_to_csv(f"{topic_name}_trends.csv", topic_news)
```

## Adding Custom Sources

To add a new news source:

```python
def parse_custom_site(self, url: str, max_articles: int = 20):
    """Parser for your website"""
    response = self.session.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')
    
    articles = []
    items = soup.select('your.selector')
    
    for item in items[:max_articles]:
        title = item.select_one('h2').get_text(strip=True)
        link = item.select_one('a')['href']
        
        article = NewsArticle(title=title, url=link, source="Custom Site")
        articles.append(article)
    
    return articles
```

## Export Formats

### CSV Format
```csv
title,url,description,date,category,source
"News Title","https://...","Description","2024-11-27","Tech","BBC News"
```

### JSON Format
```json
{
  "total": 20,
  "timestamp": "2024-11-27T10:30:00",
  "articles": [
    {
      "title": "News Title",
      "url": "https://...",
      "description": "Description",
      "date": "2024-11-27",
      "category": "Tech",
      "source": "BBC News"
    }
  ]
}
```

### HTML Format
Professional HTML document with all articles, styled with CSS.

## Limitations and Notes

### Rate Limiting
Some websites may limit request frequency. Add delays:

```python
import time

for url in urls:
    articles = parser.parse_generic_news(url)
    time.sleep(2)  # 2 second pause
```

### Robots.txt
Always check the website's robots.txt before scraping:
```
https://example.com/robots.txt
```

### User-Agent
The parser uses a standard browser User-Agent for proper functioning.

## Error Handling

The script handles various error scenarios:
- Connection failures
- Invalid HTML structure
- Missing elements
- Timeout errors
- Invalid URLs

All errors are logged with detailed information.

## Troubleshooting

### Connection errors
- Check internet connection
- Verify website is accessible
- Check for firewall issues

### No articles found
- Verify website structure hasn't changed
- Check CSS selectors
- Try generic parser

### Encoding issues
- Specify encoding explicitly
- Use utf-8-sig for CSV files

## Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/NewSource`
3. Commit changes: `git commit -m 'Add new news source'`
4. Push to branch: `git push origin feature/NewSource`
5. Open Pull Request

## License

MIT License - see LICENSE file for details

## Author

Your Name
GitHub: github.com/your_username
Email: your@email.com

## Acknowledgments

- requests - HTTP library for Python
- BeautifulSoup - HTML parsing library
- lxml - fast XML and HTML parser

## Support

For issues or questions:
- Create an issue on GitHub
- Email: nazarijsevcuk69@gmail.com

## Related Projects

- Telegram ToDo Bot - Task management bot
- Excel Automation - Automated Excel processing
- Text Analyzer - Text analysis with visualization
- Currency API - Currency conversion service

---

Last updated: November 2025
Version: 1.0
Status: Production Ready
