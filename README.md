#URL Hashing System
## Architecture

I would choose to implement this URL hashing system as a REST API using the PHP Laravel framework. Laravel provides a great deal of built-in functionality for handling HTTP requests, routing, and database interactions, which will make it easier to build this application.

The core of the URL hashing system will be a hash function that takes an input URL and generates a unique, shortened hash. This hash will be stored in a database along with the original URL. When a request is made for the hashed URL, the application will look up the original URL in the database and redirect the user to it.

In order to track clicks, I will store the number of clicks for each hashed URL in the database and increment it every time the URL is accessed. I will also store the date the URL was created and when it was last clicked(accessed).

## Setup
1. Clone the repository to your local machine 
`git clone https://github.com/prashant12it/url-hashing-system.git
`
2. Change into the newly created directory `cd url-hashing-system
`
3. Install dependencies `composer install
`
4. Copy the example environment file and configure your database settings `cp .env.example .env
`
5. Generate an application key `php artisan key:generate
`
6. Run database migrations `php artisan migrate
`
7. Start the development server `php artisan serve
`
## TODO

- Store hashed URLs and their metadata in a separate database table with appropriate access controls to make the generated URLs privacy-aware
- Add tests for URL hashing functionality
- Add authentication for accessing click tracking data
- Implement expiration for hashed URLs
- Implement UI for generating hashed URLs
## Assumptions
- The input URL does not contain any malicious characters that would break the hash function.
- The target server is running PHP 7.4 or higher.

## API Endpoints

The following endpoints will be available for the URL hashing system:
### 1. Hash a URL

**POST** `/generate-hash`

**Request Body**

`{
     "url": "https://www.newsatic.com/news/proposed-changes-in-new-tax-regime/"
 }
`

**Response**

`{
     "hash": "http://127.0.0.1:8000/809efd"
 }`
 
 ### 2. Redirect to Original URL
 
 **GET** `/{hashed_url}`
 
 **Response**
 
 Redirects to the original URL associated with the given hashed_url.
 ### 3. Get Click Data
 
 **GET** `/get-click-report/{hash}`
 
 **Response**
 
 `{
      
      "original_url": "https://www.newsatic.com/news/proposed-changes-in-new-tax-regime/",
      "hash_url": "http://127.0.0.1:8000/809efd",
      "total_clicks": 2,
      "last_clicked": "2023-02-03 11:27:32"
  }`
## Deployment

Assuming you have a server with PHP and a web server (such as Apache or Nginx) installed, you can deploy the URL hashing system using the following steps:

1. Copy the contents of the url-hashing-system directory to your server.
2. Configure your web server to serve the contents of the public directory as the document root.
3. Set the necessary environment variables, such as the database connection settings, on the server.
4. Run the necessary database migrations.
