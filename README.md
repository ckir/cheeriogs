# cheerio for Google Apps Script

This project is unofficial update of https://github.com/tani/cheeriogs.

Difference to the project is follows.

- Using webpack with [gas-webpack-plugin](https://github.com/fossamagna/gas-webpack-plugin)
- Updating [cheerio](https://github.com/cheeriojs/cheerio) to ^1.0.0-rc.12
- Exporting the function `cheerioLoad` as same as `cheerio.load`
- Exporting the function `cheerioText` as same as `cheerio.text`


## Adding the library to your project
I'm not using this as library due to this warning from Google

Warning: A script that uses a library doesn't run as quickly as it would if all the code were contained within a single script project. Although libraries can make development and maintenance more convenient, use them sparingly in projects where speed is critical. Because of this issue, library use should be limited in add-ons.

So instead I prefer to add a code file to my project and copy/paste the contents of dist/index.js into that file

## Usage

```js
let $ = cheerioLoad('This is <em>content</em>.');
let title = cheerioText($('body'));
```

### Returns This is content.

```js
  const content = getContent_('https://en.wikipedia.org');
  const $ = cheerioLoad(content);
  Logger.log($('#mp-right').text());
```

### Returns the content of the first paragraph `<p>` of Wikipedia's Main Page

```js
  const content = getContent_('https://en.wikipedia.org');
  const $ = cheerioLoad(content);
  Logger.log($('p').first().text());
```

### Changes the content of the gas server part before hosting. **!Do not do this. But you can.**

```js
  const html = HtmlService.createHtmlOutputFromFile("index").getContent();
  const $ = cheerioLoad(html);
  $("#main").append("<p>Cheeriosse!!1</p>");
  return HtmlService.createHtmlOutput(
    Utilities.formatString("<html>%s</html>", $('html').html())
  );
```

## FAQ

### Why can not I debug my code?

The latest Google App Script uses V8 runtime.
Version 12 of Cheeriogs supports the runtime.
Please upgrade your script. Then, you can do it.

## Sponsorship

This project is maintained by volunteers.
If you are using this project where it is important,
consider one time or regular donations, please.

- [❤️ GitHub Sponsors (@tani)](https://github.com/sponsors/tani)
