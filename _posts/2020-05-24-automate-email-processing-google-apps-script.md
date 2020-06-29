---
title: Automate your email processing with Google Apps Script
tags:
  [
    google,
    apps,
    script,
    javascript,
    gmail,
    spreadsheet
  ]
excerpt: How to read your bill email data and create a row in an Spreadsheet automatically.
lang: en
ref: automate-email
---

Bill Gates is often credited with the quote, *“I will always choose a lazy person to do a difficult job because a lazy person will find an easy way to do it.”*

I hate doing manual tasks that a machine would do faster and with less errors. I keep track of expenses (water, electricity, etc.) in a Google SpreadSheet that I fill every month, this way I can see my average cost, year cost...I love data, what can I say?

Recently I discovered [Google Apps Script](https://developers.google.com/apps-script). It allows you to create javascript code that can automatize all the apps under Google Apps. You can even create a chat bot, but I wanted just to parse data from an email and write it in a sheet, far-less ambituous.

Something that can be improved is the online editor...I would love to edit the script locally and then push it (repo style) but it only works with an online editor. I ended up coding a Node app and the copy pasting the code.

## Reading email

To read email, after going through the [Gmail Service Reference](https://developers.google.com/apps-script/reference/gmail) I started tagging automatically the emails I wanna read in the script so later they are easy to find:

  `var label = GmailApp.getUserLabelByName("TAG_NAME");`

Then I just pick the unread threads:

  `var threads = label.getThreads().filter(t => t.isUnread());`

Now I iterate through all the unread emails, get the first email in the thread (there is only one when you receive a bill from your company) and then I get the date, get the plain text and split the lines.:

```
threads.forEach(thread => {
  var message = thread.getMessages()[0];
  var date = message.getDate().toLocaleString('en-us', {year: 'numeric', month: '2-digit', day: '2-digit'});
  var body = message.getPlainBody();
  var bodyLines = body.split('\n');
  ...
```

Once here it's all your choice, I use `findIndex`, `replace`, `filter` to get the data and create a little object with date, money and consumption (kWh).

As a final step, to prevent the script to get the same email again and again I mark it as read and archive it:

```
thread.markRead();
thread.moveToArchive();
```

## Adding row to SpreadSheet

The [Spreadsheet Service Reference](https://developers.google.com/apps-script/reference/spreadsheet) is very similar. First we have to open the Spreadsheet and then the sheet, [the spreadsheet id can be retrieved from the URL](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#openbyidid).

```
var spreadSheet = SpreadsheetApp.openById(SPREADSHEET_ID);
var sheet = spreadSheet.getSheetByName(SHEET_NAME);
```

Then you have to create and array with the data you got in previous email step and add it:

`sheet.appendRow([DATA,DATA2,DATA3]);`

This will add a row in the first empty row of your sheet. If you wanna leave empty cells before the data, you can use empty string `''`, here I have 3 empty cells before a cell with data: `['','','',DATA]`. In the reference you have methods available for inserting the row in a specific position if needed.

## Triggers

Once the script is ready, you have to configure when you want to run it. In the [triggers view](https://script.google.com/home/triggers) I configured it to run daily at 5am.

Any ideas for more scripts?
