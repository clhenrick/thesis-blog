---
layout: post
title: Data Scraping
date: 2014-10-06
summary: Scraping NYC tax-lot transaction records.
categories: technical-module prototypes
---
Recently I assisted a local housing / tenets' rights group with retrieving property transaction data for my neighborhood in Brooklyn. The data is hosted by the NYC department of finace on a web portal called ACRIS. The problem with accessing this data is that you need to know specific numbers that designate a property's borough, block and lot. Even then you may only access one property's transaction records at a time and cannot output the data to a usable format such as an excel or CSV table. 

In order to grab the property transaction records for the 30 some properties the group requested, I wrote a Python script that reads a CSV of properties that have been extracted from the NYC Map-PLUTO dataset (this is geospatial data representing tax-lot boundaries that contains the numbers for blocks, lots and boroughs as well as addresses and other information for all parcels/tax-lots in NYC). I extracted the map-PLUTO data by using a GIS to select the appropriate tax-lots based on their geographic location. I then exported these selected parcels to a CSV file that could be read by Python and used for retrieving the necessary block and lot numbers for the data scraping process.

## Process:
1. Using QGIS and the Map-PLUTO data, extract property (tax lot) data based on a desired geographic location that has been pre-determined.
2. Save the property data as a CSV file and open it with Python.
3. Iterate over the CSV to grab the address, block and lot numbers for each property.
4. Create a dictionary object in Python with these values to create data necessary for an HTTP POST request.
5. Perform a POST request on the ACRIS URL (http://a836-acris.nyc.gov/DS/DocumentSearch/BBLResult) passing with it both header information (this specifies a browser) and the data containing borough, block and lot numbers.
6. Separate each request by random time interval to mimic browser behavior to prevent being blocked by the server.
7. Scrape values from the HTML table returned by ACRIS using the Beautiful Soup library in Python.
8. Output the table data for each property to a CSV file.

## Code
Here is the script I wrote in a hurry to accomplish the above task:
<pre><code>
from sys import argv
import csv
import requests
import bs4
import time
import random

script, filename = argv

url = "http://a836-acris.nyc.gov/DS/DocumentSearch/BBLResult"
headers = {'User-Agent' : 'Mozilla/5.0'}

count = 0

with open(filename, 'rb') as f:
    reader = csv.reader(f)
    next(reader, None)

    try:
        for row in reader:
            print row
            # example url from arcis http://a836-acris.nyc.gov/bblsearch/bblsearch.asp?borough=3&block=1306&lot=35
            block = row[1]
            lot = row[2]
            address = row[11]
            #print  "the block is %s and the lot is %s" % (block, lot)
            url2post = "http://a836-acris.nyc.gov/bblsearch/bblsearch.asp?borough=3&block=%s&lot=%s" % (block,lot)
            print "the address is %s and the url is: %s" % (address, url2post)

            data = {
                'hid_borough':'3', 
                'hid_borough_name':'BROOKLYN / KINGS', 
                'hid_block':block, 
                'hid_block_value': block, 
                'hid_lot':lot, 
                'hid_lot_value': lot,
                'hid_doctype_name':'All Document Classes',
                'hid_max_rows':'10',
                'hid_page':'1',
                'hid_SearchType':'BBL',
                'hid_ISIntranet':'N'
            }

            # make sure the POST data looks good
            print data

            t = open(address + ".csv", 'w+')

            # write column headers
            t.write("Reel/Pg/File,CRFN, Lot, Partial, Doc Date, Recorded / Filed, Document Type, Pages, Party1, Party2, Party3 / Other, More Party 1/2 Names, Corrected / Remarks, Doc Amount\n")

            response = requests.post(url, headers=headers,data=data)
            soup = bs4.BeautifulSoup(response.text)

            # print the response to see what was returned
            print response

            # find the correct part of the HTML table returned by ACRIS
            table = soup.find(attrs={"cellspacing":"1","width":"100%"})

            # iterate over table to grab the necessary values and write them to a CSV
            for row in table.find_all('tr')[1:]:
                
                for col in row.find_all('td')[1:]:
                    # f = col.find_all('font')                    
                    for f in col.find_all('font'):
                        value = f.string
                        print value                                               
                        try:                           
                            # print value.strip()
                            value = value.replace(',','')
                            t.write(value.strip())
                            t.write(',')                                    
                        except Exception:
                            t.write('*,')
                            pass
                        count +=1
                    if count !=0 and count % 14 == 0:
                        t.write('\n')

            t.close()

            # pause the script for a random interval 
            time.sleep(random.randrange(32,48))

    except csv.Error as e:
        sys.exit('file %s, line %d: %s' % (filename, reader.line_num, e))
</code></pre>

## Refinement
As I created this code fairly quick it would be good to refactor it and create a python module from it. This way the script could be used in a web app where a user could select the desired tax lots from a map to retrieve CSV's of transaction records for each selected lot. This will likely become inspiration for me to make my first Django web application with Python, something I've been meaning to explore for some time now.