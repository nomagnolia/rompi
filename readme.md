# Who Pays Your MP
Who Pays Your MP is an attempt to democratise the extra income data for MPs in the UK, by scraping, indexing and conforming publicly-available data from a number of sources. The front end lives at [whopaysyourmp.com](https://whopaysyourmp.com).

## Table of contents
* [Data sources](#data-sources)
* [Observations](#observations)
* [Systems to Create](#systems-to-create)
* [Suggested Technologies](#suggested-technologies)
* [Wishlist](#wishlist)
* [Contributing](#contributing)
* [License](#license)

## Data sources
1. [The Register of MPs' Interests](https://publications.parliament.uk/pa/cm/cmregmem/contents2122.htm)
2. [Current list of MPs](https://members.parliament.uk/members/Commons)
3. [MP salary data](https://www.theipsa.org.uk/mp-costs/mps-pay-and-pensions/)
4. (Optional) - [Companies House API](https://developer.company-information.service.gov.uk/)
5. Other sources to find out who donors are: LinkedIn, twitter, news articles etc.

## Observations
1. Scraping the Register itself is reasonably straightforward. The latest register on the page linked to in (1) above is currently the link from the first "HTML Version" text - `<a href="220131/contents.htm">HTML version</a>` on line 108, as at 11 Feb 2022. From this link, the link after the first occurrence of an `<h3>` tag takes you to the first MP (Diane Abbott). Extracurricular income is then listed in sections, which are explained in the [Code of Conduct](https://publications.parliament.uk/pa/cm201719/cmcode/1882/188201.htm) (which is of course subject to change).
    1.  Actually making sense of this data is the challenge. It's not in any kind of standard format, and so we will need to be very careful when parsing it to make sure we're not allowing any errors to slip in.
    2.  Numerical amounts are often entered wrongly, such as "£3,173,67" (Chris Clarkson) which should obviously end up as 3173.67 and not 317,367.
    3.  Donations in kind will be tricky to quantify.
    4.  Category 6 (property) might tell us nothing useful, as MPs don't even have to declare property interests below a certain threshold and we would have to comb through Land Registry records to find ownership details.
2.  This list is easier to scrape, and will be useful to provide an MP's party affiliation as well as a thumbnail pic.
3.  Salaries are updated (I think) yearly.
4.  The Companies House API allows a max of [600 requests per five minutes](https://developer.company-information.service.gov.uk/developer-guidelines/) - 2 per second. With 650 MPs, some of whom don't declare any extra income, this shouldn't be a limiting factor, although CH data is notoriously crappy.
5.  This is a very manual step.

## Systems to create
1. The scrapers
2. API interface to CH
3. Data manipulation of the scraped HTML
4. A database to store everything in
5. A backend, to streamline the process of conforming, matching and assigning the data to various sources
6. A frontend

## Suggested Technologies
* R 
* PHP
* MySQL

## Wishlist
* A backend which allows flexibility when assigning currency amounts to different sources
* The DB should hold donor information (both private individuals and companies) and keep a paper trail of edits
* Eventually, a Wikipedia-style interface that allows signed-in users to contribute (with a full audit trail of course)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
