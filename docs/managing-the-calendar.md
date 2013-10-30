# Managing the Calendar

## Configuring Your Site

### Site URL & Page Extensions

When setting up the Calendar Site, the default Site URL and Page extension values may need to be replaced.

The Site URL is specified in the following locations:

- Cascade Site Management -> Site URL
- `/_cascade/formats/outputs/rss/rss20 - event listing`
- `/_cascade/formats/outputs/rss/xhtml2fo2pdf - event listing`

The Default Page Extensions (ie .html, .php, .aspx) are specified in the following locations:

- Site Management -> Configuration Sets -> (any Configuration Set with HTML)
- `/_cascade/formats/outputs/rss/rss20 - event listing`
- `/_cascade/formats/outputs/rss/xhtml2fo2pdf - event listing`
- `/_cascade/formats/outputs/xml/events xml`

### Using a sub-folder

Although the provided examples are intended to be stand-alone Sites, the calendar may also be placed within a sub-folder of a Site. When using a sub-folder, the following should be updated: 

- All Format import and include directives (Velicty and XSLT) must be updated to correspond to the Asset's new location
- Paths to File Assets referenced within Formats should be updated (e.g. `<script>` tags within the `/_cascade/formats/external-sources-js` Formats)
- Formats containing a variable for Site path or folder prefix should be updated to correspond to the Asset's new location
  - `/_cascade/formats/outputs/xml/events xml`
  - `/_cascade/formats/outputs/pdf/rss20 - event listing`
  - `/_cascade/formats/full calendar script`

**Note:** The Site URL and page extensions should still be configured as mentioned previously.


### Configuration Sets

**DO NOT** change the default Configuration for the `YYYY/index` and `YYYY/MM/index` pages. Changing the default Configuration will cause the AJAX for the Full Calendar to break due to the way the paths to these pages are constructed. Also, avoid renaming Configuration names to avoid potential issues with `[system-asset:configuration]` pseudo tags.

### iCal Output Time Zone

The iCal output is based on the [time zone](http://en.wikipedia.org/wiki/Time_zone) for your location. Adjusting the time zone requires changing the following variables within the `/_cascade/formats/outputs/ical/ical - minified` Format:
- `$tzName` - the name of the time zone (default: **America/New_York**)
- `$tzStandard` - the standard time abbreviation and offset of the time zone (default: **EST** and **-0500**)
- `$tzDaylight` - the daylight savings time abbreviation and offset of the time zone (default: **EDT** and **-0400**)

## Publishing Events

Aside from an event's details page, there are multiple references to the event that need to be published as well. After adding an event, the following pages should be published to ensure the event is listed:

- The event's details page
- The **index** page within both the event's year and month folders. For example, if an event *myevent* is within `/2012/12`, publish the following:
    - `/2012/12/myevent`
    - `/2012/12/index`
    - `/2012/index`

## Adding a New YYYY Folder

To create a folder for a new year:
- Use New Menu -> Yearly Events Folder
- Enter the year into the folder’s *Title* field (in YYYY format).
- Edit the *index* page within your newly created folder
- Enter the desired text into the *Title* field
- Follow the *Publishing Events* instructions above

**Note:** After adding a new year (and events), it is easiest to publish the entire year folder along with the Full Calendar page. Alternatively, you can publish individual pages by following the instructions under **Publishing Events**.

## Categories

Categories allow you to easily group events by a common taxonomy. Categories can be used to color code events on the Full Calendar, create upcoming event listings and even create an Academic Calendar using a term listing page.

*Included Categories:* Campus Events, Academics, Alumni, Holidays, Students

### Updating Categories

A few modifications are required to update the categories that are used when creating events, listing events by category, viewing categories on the full calendar.

#### Metadata Sets

The *categories* dropdown must be modified within the following Metadata Sets:

- Category Listing
- Event

**Note:** If a category is removed, category listing pages using the removed category will no longer display events with that category.

### Data Definition

The **Color Mapping** Data Definition must be updated so the *Category* dropdown reflects the values of those entered within the Metadata Sets above.

### Color Mapper

In order for the categories to be color coded, the block located at `/_cascade/_calendar/category-colors-mapping/default-colors` should be modified so that each Category is given a CSS class and color. This block is used to generate a CSS `<style>` tag at the top of the full calendar and event details pages.

**Note:** If any category is renamed, existing events and color mappings must be updated to reflect the new category value. The category colors should be in hex or color name format. For example, `#000`, `#a32929` or `green`.