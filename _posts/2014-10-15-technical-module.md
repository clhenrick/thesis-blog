---
layout:     post
title:      Technical Module
date:       2014-10-15
summary:    Slides, prototype and design brief for the technical module.
categories: technical-module presentations
---
*last updated 10/19/14*

## Slides
Slide show available [here]({{site.url}}/assets/technical-present/index.html)

## Prototype

### Scraping ACRIS with Python:  

![]({{site.url}}/assets/technical-present/img/acris-transaction-data.png)
*Sample HTML table obtained from ACRIS through a POST request.*

![]({{site.url}}/assets/technical-present/img/empire_flatbush_lots.png)
*Screen shot from QGIS showing study area in Prospect Lefferts Gardens.*

![]({{site.url}}/assets/technical-present/img/map-pluto-csv-data.png)  
*Sample of data outputted from Map-PLUTO using QGIS:*

###Final Python code used for ACRIS web scraping:  

    from sys import argv
    import csv
    import requests
    import bs4
    import time
    import random

    script, filename = argv

    # f = open(filename)

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
                print data

                t = open(address + ".csv", 'w+')
                # write column headers
                t.write("Reel/Pg/File,CRFN, Lot, Partial, Doc Date, Recorded / Filed, Document Type, Pages, Party1, Party2, Party3 / Other, More Party 1/2 Names, Corrected / Remarks, Doc Amount\n")

                response = requests.post(url, headers=headers,data=data)
                soup = bs4.BeautifulSoup(response.text)
                print response

                table = soup.find(attrs={"cellspacing":"1","width":"100%"})

                # iterate over table
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
                time.sleep(random.randrange(32,48))
        except csv.Error as e:
            sys.exit('file %s, line %d: %s' % (filename, reader.line_num, e))
    



### Building off of the ACRIS data scraping to design a map based UI:

![]({{site.url}}/assets/nyc_extractor01.png)
*Landing page for the UI*

![]({{site.url}}/assets/nyc_extractor02.png)
*Zooming in to select a lot*

![]({{site.url}}/assets/nyc_extractor03.png)
*Hovering on a lot reveals basic info*

![]({{site.url}}/assets/nyc_extractor04.png)
*Drawing a rectangle to select lots to retrieve transaction history*

### To Do:
- refine the UI, eg: toggling the tax-lot selection, displaying retrieved tables, etc.
- Implement the Backend part of the app that stores the tables for lot transaction histories and retrieves data based on the user's query.

## Design Brief
A PDF of the design brief is available [here]({{site.url}}/assets/technical-module-design-brief.pdf)
