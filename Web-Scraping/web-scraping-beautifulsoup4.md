# Notes

[Article Link](https://www.dataquest.io/blog/web-scraping-python-using-beautiful-soup/)

## What is Web Scraping?
1. Some websites offer datasets that are downloadable in CSV format, or accessible via an `Application Programming Interface` ( API )
1. Many websites with useful data don't offer those convenient options 
1. Web scraping is a technique that lets us use programming to do the heavy lifting 
1. We'll write some code that looks at the site, grabs just the data we want to work with, ans outputs it in the format we need 

## How does web scraping work?
1. When we scrape the web, we write code that sends a request to the server that's hosting the page we specified
1. The server will return the source code-HTML, mostly for the page or pages we requested
1. So far, we're essentially doing the same thing a web browser does - sending a server request with a specific URL and asking the server to return the code for that page
1. But unlike the web browser, our web scraping code won't interpret the page's source code and display the page visually
1. Instead, we'll write some custom code that filters through the page's source code looking for specific elements we've specified, andnd nssandd# Notes

## What is Web Scraping?
1. Some websites offer datasets that are downloadable in CSV format, or accessible via an `Application Programming Interface` ( API )
1. Many websites with useful data don't offer those convenient options 
1. Web scraping is a technique that lets us use programming to do the heavy lifting 
1. We'll write some code that looks at the site, grabs just the data we want to work with, ans outputs it in the format we need 

## How does web scraping work?
1. When we scrape the web, we write code that sends a request to the server that's hosting the page we specified
1. The server will return the source code-HTML, mostly for the page or pages we requested
1. So far, we're essentially doing the same thing a web browser does - sending a server request with a specific URL and asking the server to return the code for that page
1. But unlike the web browser, our web scraping code won't interpret the page's source code and display the page visually
1. Instead, we'll write some custom code that filters through the page's source code looking for specific elements we've specified, and extracting whatever content we've instructed it to extract 
1. For e.g., if we wanted to get all of data from inside a table that was displayed on a web page, our code would be written to go through these steps in sequence
	1. Request the content( source code ) of a specific URL from the server
	1. Download the content that is returned 
	1. Identify the elements of the page of the table we want 
	1. Extract and( if necessary) reformat those elements into a dataset we can analyze or use in whatever way we require
1. One thing important to note: from a server's perspective, requesting a page via web scraping is the same as loading it in a web browser
1. When we use code to submit these requests, we might be "loading" pages much faster than a regular user, and thus quickly eating up the website owner's server resources

## Is web scraping legal?
1. Unfortunately, there's not a cut and dry answer
1. Some websites explicitly allow web scraping. Others explicitly forbid it. Many websites don't offer any clear guidance one way or another

## Web Scraping Best Practices
1. Never scrape more frequently than you need to
1. Consider `caching` the content you scrape so it's only downloaded once 
1. Build pauses into code using functions like `time.sleep()` to keep from overwhelming servers with too many requests too quickly 


## The components of a Web Page
1. When we visit a web page, our web browsers makes a request to web server. This request is called a `GET` request, since we're getting files from the server 
1. The server then sends back files that tell our browser how to render the page for us 
1. These files will typically include
	1. `HTML` - the main content of the page
	1. `CSS` - used to add styling to make the page look nicer 
	1. `JS` - Javascript files add interactivity to web pages
	1. Images - image formats, suck as `JPG` and `PNG`, allow web pages to show pictures
1. After our browser receives all the files, it renders the page and display it to us
1. When we perform web scraping, we're interested in the main content of the web page, so we look primarily at the HTML 

## HTML 
1. `HyperText Markup Language` is the language that web pages are created in
1. HTML isn't a programming language, like Python
1. It's a **markup language** that tells a browser how to display content 

## The requests library 
1. The first thing we'll need to do to scrape a web page is to download the page
1. We can download the web pages using the Python `requests` library
1. The requests library will make a `GET` request to a web server, which will download the HTML contents of the a given web page for us 
1. After running our request, we get `Response` object
1.This object has a `status_code` property, which indicates the page was downloaded successfully 
1. A `status_code` of `200` means that the page downloaded successfully
1. Status code starting with `2` generally indicated success, and a code starting with a `4` or `5` indicates a error
1. We can print out the HTML content of the page using the `content` property 

## Parsing the page with BeautifulSoup 
1. We can use the `BeautifulSoup` library to parse this document, and extract the text from the `p` tag
1. We first have to import the library, and create an instance of the `BeautifulSoup` class to parse our document
```
from bs4 import BeautifulSoup
soup = BeautifulSoup(page.content, 'html.parser')
```
1. We can now print out the HTML content of the page, formatted nicely, using the `prettify` method on the `BeautifuSoup` object
```
print(soup.prettify())

```
1. As all of the tags are nested, we can move through the structure one level at a time 
1. We can first select all the elements at the top level of the page using the `children` property of `soup`
1. All of the items are	`BeautifulSoup` objects 
	1. The first is a `Doctype` object, which contains the information about the type of the document 
	1. The second is a `NavigatableString`, which represents text found in the HTML document
	1. The final item is a `Tag` object, which contains other nested tags
1. The most important object type, and the one we'll deal with most often, is the `Tag` object 
1. The `Tag` object allows us to navigate through an HTML document, and extract other tags and text
1. We can now select the `html` tag and its children by taking the third item in the list
1. Now we, can get the `p` tag by finding the children of the body tag 
1. We can now isolate the p tag
1. Once we've isolated the tag, we can use the get_text method to extract all of the text inside the tag

## Finding all instances of a tag at once 
1. If we want to extract a single tag, we can instead use the `find_all` method, which will find all the instances of a tag on a page
1. Note that `find_all` returns a list, we'll have to loop through, or use list indexing, it to extract text
1. If you instead only want to find the first instance of a tag, you can use the `find` method, which will return a single `BeautifulSoup` object

# Searching for tags by class and id 
1. Classes and ids are used by CSS to determine which HTML elements to apply certain styles to 
1. But when we're scraping, we can also use them to specify the elements we want to scrape

## Using CSS selectors
1. We can also search for items using `CSS selectors`
1. These selectors are how the CSS language allows developers to specify HTML tags to style 
1. `BeautifulSoup` objects support searching a page via CSS selectors using the `select` method 

## Time to start scraping
1. Steps to scraping the website
	1. Download the web page containing the forecast
	1. Create a `BeautifulSoup` class to parse the page
	1. Find the `div` with id `seven_day_forecast`, and assign to `seven_day`
	1. Inside `seven_day`, find each individual forecast item 
	1. Extract and print the first forecast item 

## Extracting information from the page
1. As we can see, inside the forecast item `tonight` is all the information we want
1. There are four pieces of information we can extract 
	1. The name of the forecast item - in this case, Tonight
	1. The description of the conditions - this is stored in the title property of img
	1. A short description of the conditions - in this case Mostly Cloud
	1. The temperature low - in this case, 57 degrees

## Extracting all the information from the page
1. Steps 
	1. Select all the items with the class period-name inside an item with the class tombstone-container in seven_day
	1. Use a list_comprehension to call the get_text method on each BeautifulSoup object

## Combining our data into a Pandas DataFrame 
1. We can now combine the data into a `Pandas` DataFrame and analyze it
1. A DataFrame is an object that can store tabular data, making data analysis easy 
1. In order to do this, we'll call the DataFrame class, and pass in each list of items that we have. We pass them in as part of the dictionary
1. Each dictionary key will become a column in the DataFrame, and each list will become the values in the column 
