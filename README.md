# Calendar-Examples.csse

Features include:

* Interactive calendar using the [Full Calendar jQuery plugin](http://arshaw.com/fullcalendar/).
* List view for events within selected category(ies).
* List view for events defined by terms.
* Folders for yearly and monthly organization of events.
* Landing Page for events within a given year or month.
* Repeatable events using daily, weekly, monthly and yearly options.
* Multi-channel output for a variety of pages (XHTML, PDF, RSS, iCal, XML).
* Display events from external resources (Google Calendar Feed, XML, JSON, Cascade XML and Feed Blocks)

**Note:** This version makes use of the Velocity `#import` directive. For best results, import into an instance of Cascade running version 7.6 or greater; otherwise, the Formats being imported will need to be copied into the Format performing the import. Results may vary importing into 7.0.x, because of potential database structure changes and updates to how Dynamic Metadata are created/stored.

## Repeating Options

### Repeat Type

#### Daily

Repeats an event every X days (based on the interval provided).

#### Weekly

Repeats an event every X weeks (based on the interval provided).

**Repeat Weekly On** (optional) allows you to specify what day(s) of the week the repeating events should occur on. For example, every Mon, Wed, and Friday or every Tue and Thu.

#### Monthly

Repeats an event every X weeks (based on the interval provided).

**Repeat Monthly On** (optional) allows you to specify whether an occurrence falls on the exact day of the month (ie the 1st or 20th) or if it falls on the day of the week (ie the 2nd Mon or 3rd Sun).

#### Yearly

Repeats an event every X years (based on the interval provided).

### Repeat Every

The interval in which each repeating event occurs on. For example, every other day or every 3 weeks.

### Ends On

Indicates the ending point for the repeating events. If left blank, the end is 2 years from the current date.

Note: If the end date is before the next occurrence, the event will not be displayed.

## Managing the Calendar

### Configuring Your Site

#### Site URL & Page Extensions

When setting up the Calendar Site, the default Site URL and Page extension values may need to be replaced.

The Site URL is specified in the following locations:

* Cascade Site Management -> Site URL
* `/_cascade/formats/output/rss20 - event listing`
* `/_cascade/formats/output/xhtml2fo2pdf - event listing`

The Default Page Extensions (ie .html, .php, .aspx) are specified in the following locations:

* Site Management -> Configuration Sets -> (any Configuration Set with HTML)
* `/_cascade/formats/output/rss20 - event listing`
* `/_cascade/formats/output/xhtml2fo2pdf - event listing`
* `/_cascade/formats/events xml`

#### Configuration Sets

**DO NOT** change the default Configuration for the `YYYY/index` and `YYYY/MM/index` pages. Changing the default Configuration will cause the AJAX for the Full Calendar to break due to the way the paths to these pages are constructed. Also, avoid renaming Configuration names to avoid potential issues with `[system-asset:configuration]` pseudo tags.

#### iCal Output Time Zone

The iCal output is based on the [time zone](http://en.wikipedia.org/wiki/Time_zone) for your location. Adjusting the time zone requires changing the following variables within the `/_cascade/formats/output/ical` Format:
* `$tzName` - the name of the time zone (default: **America/New_York**)
* `$tzStandard` - the standard time abbreviation and offset of the time zone (default: **EST** and **-0500**)
* `$tzDaylight` - the daylight savings time abbreviation and offset of the time zone (default: **EDT** and **-0400**)

### Publishing Events

Aside from an event's details page, there are multiple references to the event that need to be published as well. After adding an event, the following pages should be published to ensure the event is listed:

* The event's details page
* The **index** page within both the event's year and month folders. For example, if an event *myevent* is within `/2012/12`, publish the following:
    * `/2012/12/myevent`
    * `/2012/12/index`
    * `/2012/index`

### Adding a New YYYY Folder

To create a folder for a new year:
* Use New Menu -> Yearly Events Folder
* Enter the year into the folder’s *Title* field (in YYYY format).
* Edit the *index* page within your newly created folder
* Enter the desired text into the *Title* field
* Follow the *Publishing Events* instructions above

Note: After adding a new year (and events), it is easiest to publish the entire year folder along with the Full Calendar page. Alternatively, you can publish individual pages by following the instructions under **Publishing Events**.

### Categories

Categories allow you to easily group events by a common taxonomy. Categories can be used to color code events on the Full Calendar, create upcoming event listings and even create an Academic Calendar using a term listing page.

*Included Categories:* Campus Events, Academics, Alumni, Holidays, Students

#### Updating Categories

A few modifications are required to update the categories that are used when creating events, listing events by category, viewing categories on the full calendar.

##### Metadata Sets

The *categories* dropdown must be modified within the following Metadata Sets:

* Category Listing
* Event

Note: If a category is removed, category listing pages using the removed category will no longer display events with that category.

#### Data Definition

The **Color Mapping** Data Definition must be updated so the *Category* dropdown reflects the values of those entered within the Metadata Sets above.

#### Color Mapper

In order for the categories to be color coded, the block located at `/calendar-libary/category-colors/category-color-mapping` should be modified so that each Category is given a CSS class and color. This block generates a CSS `<style>` tag at the top of the full calendar and event details pages.

Note: If any category is renamed, existing events and color mappings must be updated to reflect the new category value. The category colors should be in hex or color name format. For example, `#000`, `#a32929` or `green`.

## Theming the Full Calendar jQuery Plugin

The Full Calendar jQuery plugin is themable using [jQuery UI ThemeRoller](http://jqueryui.com/themeroller/).

*Included Themes:* flick, redmond

### Adding Themes

Customize and download your theme from [jQuery UI ThemeRoller](http://jqueryui.com/themeroller/) and zip the folder located within the **css** folder (this folder should contain two CSS files and an images folder). Upload the zip file into `/calendar-library/themes` using the Zip Archive tool.

### Changing Themes

Modify the block located at `/_cascade/blocks/calendar head files`. Update the CSS `<link href="/calendar-library/themes/THEME_NAME/*.css" rel="stylesheet" type="text/css"/>` tag to point to the compressed (minimized) CSS file of the desired theme.

Note: It is recommended to publish the theme folder located at `/calendar-library/themes` before publishing the Full Calendar to ensure the styles and images are available.

## External Sources

The Calendar can be configured to pull external sources into the full calendar, category listing, term listing, and year/month landing pages.

Note: Only the HTML outputs will contain the external sources. XML, RSS and iCal are not applicable because they are static files.

### Available Sources

#### RSS

An RSS feed can be pulled into the Calendar Site by adding a URL to the feed within the *URL* field or by creating a Feed Block and selecting it using the *Feed/XML Block* chooser.

#### Google Calendar Feed

Feeds from a public Google Calendar can be pulled into the Calendar Site. To locate the feed URL, open your Google Calendar, navigate to **Calendar Settings** , click on the **XML** icon and copy the address presented to you within the popup.

Note: The calendar *must* be public in order for the calendar to be able to pull in the data.

#### JSON

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


Note: The value(s) of the `className` attribute should correspond to the name of the categories within the Calendar Site. URLs containing `--` are removed to avoid render/publish issues with Cascade.

#### XML

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

Note: The value(s) of the `<category>` element should correspond to the name of the categories within the Calendar Site. URLs containing `--` are removed to avoid render/publish issues with Cascade.

### Adding/Updating External Sources

To add/update external sources edit the Structured Data Block located at `/calendar-library/external-sources/external sources`. See above for the various options.

Note: After updating the Block, the associated Pages should be republished.

### Configuring Pages to Include External Sources

Due to current limitations, the full calendar, category listing and term listing Pages have a block chooser to select the desired External Sources Structured Data Block. Year/Month landing Pages automatically include the block within the **External Source Script** Region (within the HTML Output). Update the chooser/region to point to the desired external sources Block and republish the Page(s). Alternatively, you can simply "empty" the external sources Block so it does not load anything.

### Additional Information

The external sources feature leverages [Yahoo Query Language](http://developer.yahoo.com/yql/) for consuming external sources that have a URL provided. This is to avoid the Cross Domain Policy restriction of AJAX requests. A custom plugin, `/_files/scripts/jquery.yqlhelper-0.1` is used to interface with YQL.

**Current Limitations**

- Current YQL restrictions require that the URLs contain a standard HTTP/HTTPS port (80/443); however, this may change in the future.
- YQL queries are cached for 15 minutes to avoid rate limit issues. To change this timeframe, pass `maxAge` (in seconds) within the options for `$.YQL.query()`.

# Calendar-Clean.csse

Calendar-Clean.csse has no example events and is stripped of most customizations including headers, footers, and logos.

## list-events.vm

This will pull events (create a Content Type Index Block first) into another Site for showing upcoming events from the calendar. Note: External sources are not applicable.

## sort-events.xml

This XSLT is applied at either the Template or Configuration Set Level to sort those events being pulled into other Sites.
