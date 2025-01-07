
# Ultimate Guide to Using Web Scraper for Amazon Data Extraction: Extract QA, Reviews, and More

## Introduction

Before you begin, ensure that you have the **Web Scraper** extension installed on your browser. Once set up, you can follow these examples to scrape various types of Amazon data efficiently.

---

## Methods for Scraping Pages

You have two primary options for data extraction:

1. **Scrape All Pages**: Automate pagination to extract data from all pages.
2. **Scrape Specific Pages**: Manually specify the number of pages you want to scrape.

### Example 1: Scrape All QA Pages

This method automates pagination to extract QA data from all pages of a product.

#### Code:
```json
{
  "_id": "amz-qa",
  "startUrl": ["https://www.amazon.com/ask/questions/asin/B09FT58QQP"],
  "selectors": [
    {
      "id": "contents",
      "parentSelectors": ["_root", "nextpage"],
      "type": "SelectorElement",
      "selector": ".a-section > div.a-spacing-base > div > div.a-col-right",
      "multiple": true,
      "delay": null
    },
    {
      "id": "question",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": ".a-spacing-small div.a-col-right",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "answer",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": ".a-col-right > span:nth-of-type(1)",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "buyer",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": "span.a-profile-name",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "date",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": "span.a-color-tertiary",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "nextpage",
      "parentSelectors": ["_root", "nextpage"],
      "type": "SelectorLink",
      "selector": ".a-last a",
      "multiple": true,
      "delay": 0
    }
  ]
}
```

After importing the code into Web Scraper, edit the settings to scrape specific pages if needed. Replace the ASIN in the URL to target different products.

---

### Example 2: Scrape QA for Specific Pages

If you only need data from a limited number of pages, you can specify the range in the URL.

#### Code:
```json
{
  "_id": "amz-qa2",
  "startUrl": ["https://www.amazon.com/ask/questions/asin/B09FT58QQP/[1-8]"],
  "selectors": [
    {
      "id": "contents",
      "parentSelectors": ["_root"],
      "type": "SelectorElement",
      "selector": ".a-section > div.a-spacing-base > div > div.a-col-right",
      "multiple": true,
      "delay": null
    },
    {
      "id": "question",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": ".a-spacing-small div.a-col-right",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "answer",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": ".a-col-right > span:nth-of-type(1)",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "buyer",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": "span.a-profile-name",
      "multiple": false,
      "delay": 0,
      "regex": ""
    },
    {
      "id": "date",
      "parentSelectors": ["contents"],
      "type": "SelectorText",
      "selector": "span.a-color-tertiary",
      "multiple": false,
      "delay": 0,
      "regex": ""
    }
  ]
}
```

---

## Advertisement

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Scrape Competitor Reviews

This method extracts review details, such as reviewer names, scores, content, and dates.

#### Code:
```json
{
  "_id": "review",
  "startUrl": ["https://www.amazon.com/Insulated-Lunch-Bag-Women-Men/dp/B07WVWSVL3/ref=cm_cr_arp_d_viewopt_sr?ie=UTF8&reviewerType=all_reviews&pageNumber=1&filterByStar=all_stars"],
  "selectors": [
    {
      "id": "info",
      "type": "SelectorElementClick",
      "selector": ".a-row div.celwidget",
      "multiple": true,
      "parentSelectors": ["_root"],
      "clickElementSelector": ".a-last a",
      "clickElementUniquenessType": "uniqueCSSSelector",
      "clickType": "clickMore",
      "delay": 3000,
      "discardInitialElements": "do-not-discard"
    },
    {
      "id": "name",
      "type": "SelectorText",
      "selector": "span.a-profile-name",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "score",
      "type": "SelectorText",
      "selector": "> div:nth-of-type(2)",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "status",
      "type": "SelectorText",
      "selector": "div.a-spacing-mini.review-data",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "time",
      "type": "SelectorText",
      "selector": "span.a-color-secondary",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "content",
      "type": "SelectorText",
      "selector": "div.a-spacing-small",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    }
  ]
}
```

---

## Scrape Search Results (Keywords and Products)

### Infinite Pagination
This code handles continuous pagination to scrape data from all search results.

#### Code:
```json
{
  "_id": "wxsearch",
  "startUrl": ["https://www.amazon.com/s?k=lunch+box&ref=nb_sb_noss"],
  "selectors": [
    {
      "id": "info",
      "type": "SelectorElement",
      "selector": "div.s-expand-height",
      "multiple": true,
      "parentSelectors": ["_root", "panination"],
      "delay": 0
    },
    {
      "id": "title",
      "type": "SelectorLink",
      "selector": ".a-size-mini a",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0
    },
    {
      "id": "score",
      "type": "SelectorText",
      "selector": "i.a-icon-star-small",
      "multiple": false,
      "parentSelectors": ["info"],
      "regex": "",
      "delay": 0
    },
    {
      "id": "reviews",
      "type": "SelectorText",
      "selector": "span.a-size-base",
      "multiple": false,
      "parentSelectors": ["info"],
      "regex": "",
      "delay": 0
    },
    {
      "id": "panination",
      "type": "SelectorLink",
      "selector": ".a-last a",
      "multiple": true,
      "parentSelectors": ["_root", "panination"],
      "delay": 0
    },
    {
      "id": "price",
      "type": "SelectorText",
      "selector": "[data-a-size='l'] span[aria-hidden]",
      "multiple": false,
      "parentSelectors": ["info"],
      "regex": "",
      "delay": 0
    }
  ]
}
```

---

## Scrape Best Seller Lists

#### Code:
```json
{
  "_id": "amazon-com-best-sellers",
  "startUrl": ["https://www.amazon.com/Best-Sellers-Kitchen-Dining-Reusable-Lunch-Bags/zgbs/kitchen/2287321011/ref=zg_bs_pg_2?_encoding=UTF8&pg=[1-8]"],
  "selectors": [
    {
      "id": "info",
      "type": "SelectorElement",
      "selector": "div.zg-grid-general-faceout",
      "multiple": true,
      "parentSelectors": ["_root"],
      "delay": null
    },
    {
      "id": "name",
      "type": "SelectorText",
      "selector": "div._cDEzb_p13n-sc-css-line-clamp-3_g3dy1",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "score",
      "type": "SelectorText",
      "selector": "div.a-icon-row",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    },
    {
      "id": "price",
      "type": "SelectorText",
      "selector": "div:nth-of-type(2)",
      "multiple": false,
      "parentSelectors": ["info"],
      "delay": 0,
      "regex": ""
    }
  ]
}
```

---

## Conclusion

With this guide, you now have the tools to scrape various types of Amazon data using Web Scraper effectively. By practicing and experimenting, you’ll master web scraping in no time.

---
