<<<<<<< HEAD
# Calendar
=======
Calendar-Examples.csse
============================

For best results, import into an instance of Cascade running version 7.2 or greater. Results may vary importing into 7.0.x because of database structure changes and updates to how Dynamic Metadata are created/stored.
>>>>>>> Updated examples, added Clean version, updated README

Features include:

* Interactive calendar using the [Full Calendar jQuery plugin](http://arshaw.com/fullcalendar/).
* List view for events within selected category(ies).
* List view for events defined by terms.
* Folders for yearly and monthly organization of events.
* Landing Page for events within a given year or month.
* Repeatable events using daily, weekly, monthly and yearly options.
* Multi-channel output for a variety of pages (XHTML, PDF, RSS, iCal, XML).
<<<<<<< HEAD

**Note:** For best results, import into an instance of Cascade running version 7.2 or greater. Results may vary importing into 7.0.x because of potential database structure changes and updates to how Dynamic Metadata are created/stored.

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
=======
* Repeatable events.

Note: Calendar-Clean.csse has no example events and is stripped of most customizations including headers, footers, and logos.
>>>>>>> Updated examples, added Clean version, updated README
