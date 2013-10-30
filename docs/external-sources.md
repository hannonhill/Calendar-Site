# External Sources

The Calendar can be configured to pull external sources into the full calendar, category listing, term listing, and year/month landing pages.

**Note:** Only the HTML outputs will contain the external sources. XML, RSS and iCal are not applicable because they are static files.

## Available External Source Types

### RSS

An RSS feed can be pulled into the Calendar Site by adding a URL to the feed within the *URL* field or by creating a Feed Block and selecting it using the *Feed/XML Block* chooser.

### Google Calendar Feed

Feeds from a public Google Calendar can be pulled into the Calendar Site. To locate the feed URL, open your Google Calendar, navigate to **Calendar Settings** , click on the **XML** icon and copy the address presented to you within the popup.

**Note:** The calendar *must* be public in order for the calendar to be able to pull in the data.

### JSON

A JSON file can be pulled into the Calendar Site by supplying a URL to the file. Events should be in the format:

```
{
 "events": {
  "event": [
   {
    "id": [String/Integer. Optional],
    "title": [String. Required],
    "start": [UNIX Timestamp. Required],
    "end": [UNIX Timestamp. Optional],
    "summary": [String. Optional],
    "location": [String. Optional],
    "allDay": [Boolean. Optional],
    "url": [String. Optional],
    "className": [String/Array. Optional]
   },
   {
    ... Repeat for additional events ...
   }
  ]
  }
}
```

**Note:** The value(s) of the `className` attribute should correspond to the name of the categories within the Calendar Site. URLs containing `--` are removed to avoid render/publish issues with Cascade.

### XML

The Calendar Site can pull in XML data by adding a URL to the XML file within the *URL* field or by creating an XML Block and selecting it using the *Feed/XML Block* chooser. Events should be in the format:

```
<events>
  <event>
    <title>[String/Integer. Optional]</title>
    <title>[String. Required]</title>
    <start>[UNIX Timestamp. Required]</start>
    <end>[UNIX Timestamp. Optional]</end>
    <summary>[String. Optional]</summary>
    <location>[String. Optional]</location>
    <allDay>[Boolean. Optional]</allDay>
    <url>[String. Optional]</url>
    <categories>
        <category>[String. Optional]</category>
        ... Repeat <category> for additional categories ...
    </categories>
  </event>
  ... Repeat for additional events ...
</events>
```

**Note:** The value(s) of the `<category>` element should correspond to the name of the categories within the Calendar Site. URLs containing `--` are removed to avoid render/publish issues with Cascade.

## Adding/Updating External Sources

To add/update external sources edit the Structured Data Block located at `/_cascade/_calendar/external-sources-mapping/external-sources`. See above for the various options.

**Note:** After updating the Block, the associated Pages should be republished.

## Configuring Pages to Include External Sources

Due to current limitations, the full calendar, category listing and term listing Pages have a block chooser to select the desired External Sources Structured Data Block. Year/Month landing Pages automatically include the block within the **External Source Script** Region (within the HTML Output). Update the chooser/region to point to the desired external sources Block and republish the Page(s). Alternatively, you can simply "empty" the external sources Block so it does not load anything.

## Additional Information

The external sources feature leverages [Yahoo Query Language](http://developer.yahoo.com/yql/) for consuming external sources that have a URL provided. This is to avoid the Cross Domain Policy restriction of AJAX requests. [A custom plugin](https://github.com/rgriffith/jquery.yqlhelper), `/_files/js/plugins/jquery.yqlhelper.min.js` is used to interface with YQL.

**Current Limitations**

- Current YQL restrictions require that the URLs contain a standard HTTP/HTTPS port (80/443); however, this may change in the future.
- YQL queries are cached for 15 minutes to avoid rate limit issues. To change this timeframe, pass `maxAge` (in seconds) within the options for `$.YQL.query()`.