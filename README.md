# Keyword-Driven using TestCafe (beta)

This is the **Keyword-Driven** framework plugin for [TestCafe](http://devexpress.github.io/testcafe).

[![npm badge](https://docs.devexpress.com/TestCafeStudio/images/guides/wait-for-page-to-load.gif)]()

Testcafe Keyword Driven Framework is a type of Functional Automation Testing Framework which is also known as Table-Driven testing or Action Word based testing.

![report-sample](https://sites.google.com/site/testingbulletin/_/rsrc/1461315924116/selenium/selenium-frameworks/keyword-driven-framework/5%20column.png)

## To install this TestCafe Keyword-Driven Framework

- run the command `npm i keyword_driven`.

## Usage

- add to the testcafe command-line the following options:

```sh
testcafe chrome ./path-to-tests/*(.js)
```

## To execute the solution

       - Ensure that Node.js and npm are installed on your computer and run the following command:.

- install [testcafe](https://devexpress.github.io/testcafe/documentation/getting-started/) (version >=1.4.1):

  - `npm i -g testcafe`
  
- install [xlsx](https://www.npmjs.com/package/xlsx) (version >= 0.15.1):

  - `npm i xlsx`

- Create a `keyword-driven.js` file at the project root:

```javascript
import { Selector } from 'testcafe';
import XPath from './ComponentHelper/xpath-selector';

fixture `Getting Started`
.page `https://devexpress.github.io/testcafe/documentation/getting-started/`;

var XLSX = require('xlsx')
    var workbook = XLSX.readFile('./path-to-read/*(.xlsx)');
    var sheet_name_list = workbook.SheetNames;
    var xlData = XLSX.utils.sheet_to_json(workbook.Sheets[sheet_name_list[0]]);

    test('Keyword-Driven',  async t => {
        await t.maximizeWindow()
        for (let i = 0; i < xlData.length; i++) {
            let element = xlData[i]
            switch (element.Keyword) {
                case "navigateTo":
                    await t[element.Keyword](element.Parameter)
                    break;
                case "click":
                    await t[element.Keyword](XPath(element.LocatorValue))
                    break;
                case "typeText":
                    await t[element.Keyword](XPath(element.LocatorValue), element.Parameter)
                    break;
                case "selectText":
                    await t[element.Keyword](XPath(element.LocatorValue), element.Parameter)
                    break;
                default:
                    return;
            }
            await t.setTestSpeed(0.1)
        }
    });
```

- Create the following script in the `xpath-selector.js` file for handling `XPath`:

```javascript
import { Selector } from 'testcafe';


const elementByXPath = Selector(xpath => {
    const iterator = document.evaluate(xpath, document, null, XPathResult.UNORDERED_NODE_ITERATOR_TYPE, null )
    const items = [];

    let item = iterator.iterateNext();

    while (item) {
        items.push(item);
        item = iterator.iterateNext();
    }

    return items;
});

export default function (xpath) {
    return Selector(elementByXPath(xpath));
}
```

- run the command `testcafe chrome keyword-driven.js`



## Error rendering

- this execution will report for each file reported in the stack trace.

```
C:\ProcessDrive\TestCafe\Trails\Keyword_Driven>testcafe chrome Keyword-Driven.js
 Running tests in:
 - Chrome 76.0.3809 / Windows 10.0.0

 Getting Started
 × Keyword-Driven

   1) The element that matches the specified selector is not visible.

      Browser: Chrome 76.0.3809 / Windows 10.0.0

         21 |            switch (element.Keyword) {
         22 |                case "navigateTo":
         23 |                    await t[element.Keyword](element.Parameter)
         24 |                    break;
         25 |                case "click":
       > 26 |                    await t[element.Keyword](XPath(element.LocatorValue))
         27 |                    break;
         28 |                case "typeText":
         29 |                    await t[element.Keyword](XPath(element.LocatorValue), element.Parameter)
         30 |                    break;
         31 |                case "selectText":

         at <anonymous> (C:\ProcessDrive\TestCafe\Trails\Keyword_Driven\Keyword-Driven.js:26:27)



 1/1 failed (1m 33s)

```

## Screenshot rendering

- `Windows: .NET 4.0 (OR) Linux: ICCCM/EWMH-compliant window manager ` reporter embeds all screenshots as base 64 images, making the generated image file completely autonomous.

## Video rendering

- ` FFmpeg library` video embeds all actions as .mp4, making the generated .mp4 file completely autonomous.

## Logger rendering

- `log4js` logger embeds all information about the execution as a report, making the generated log file completely autonomous with suite of logs, Screenshots, .mp4.

## Slack notifier

- `Slack Appender for log4js-node` Sends log events to a [slack](https://slack.com) channel. This is completely autonomous with [log4js](https://log4js-node.github.io/log4js-node/). 

## Utility

- 

## Contributors

- [RemigiusLourdusamy](https://github.com/RemigiusL/)
