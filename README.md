# scp_crawler

This is a web crawler built with scrapy and designed to extract data from the SCP Wiki.

## Installation

```
make install
```

## Simple Crawl

Then to run all of the spiders and create a full data dump of the SCP Wiki and SCP International Hub in the `data` directory:

```bash
make data
```

## Custom Crawl with scrapy cli

Individual spiders with custom settings can also be called using the `scrapy` command line tool.

To show Available Spiders:

```bash
scrapy list
```

To crawl the International Hub for SCP Items and save to a custom location:

```bash
scrapy crawl scp_int -o scp_international_items.json
```

## Content Structure

There are two types of content downloaded- SCP Items and SCP Tales.

All content (both SCP Items and Tales) contain the following:

* URL
* Title
* Rating
* Tags
* Raw Content (the HTML for the story or item, without the site navigation and other boilerplate)

In addition the SCP Items include:

* SCP Identifier (ie, SCP-3000)
* SCP Number (if available)
* SCP Series
  * 1-5 (with built in support for future published series)
  * joke, explained, and decommissioned
  * Generic International (from the main site)
  * Specific Nationality Tag (from the international hub)


## Generated Files

The crawler generates a series of json files containing an array of objects representing each crawled item.

| File                | Source        | Type  | Target  |
|---------------------|---------------|-------|---------|
| goi.json            | Main          | Tale  | goi     |
| scp_items.json      | Main          | Item  | scp     |
| scp_titles.json     | Main          | Title | scp     |
| scp_tales.json      | Main          | Tale  | scp     |
| scp_int.json        | International | Item  | scp_int |
| scp_int_titles.json | International | Title | scp_int |
| scp_int_tales.json  | International | Tale  | scp_int |

Running `make TARGET` (such as `make goi` or `make scp`) will generate the site specific files. Running `make data` will fill in any missing files.

To regenerate all files run `make fresh`.


## Content Licensing

Text content on the SCP Wikis is available under the CC BY-SA 3.0 license.

This project does not download images.
