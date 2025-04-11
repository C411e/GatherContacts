# Gather Contacts
A Burp Suite Extension to pull Employee Names from Google and Bing LinkedIn and xing Search Results.

As part of reconnaissance when performing a penetration test, it is often useful to gather employee names that can then be massaged into email addresses and usernames. The usernames may come in handy for performing a [password spraying attack](http://www.blackhillsinfosec.com/?p=4694) for example. One easy way to gather employee names is to use the following Burp Suite Pro extension as described below.

You may be able to discover the username format by analyzing the metadata of documents posted to a company's public web sites as described [here](https://github.com/dafthack/PowerMeta).
To collect employee names with Burp, you'll need to do the following steps.

## Step 1
This extension uses the **jsoup** Java library. You will need to [download jsoup](https://jsoup.org/download) and tell Burp where to find it as shown below.

![Jsoup Dependency](https://github.com/clr2of8/GatherContacts/raw/master/images/jsoup.png)

Select the folder that contains the jsoup jar file, in this case I downloaded jsoup into the **C:\Users\Public\Downloads\lib** folder.

## Step 2

Add the "Gather Contacts" extension from the **Extender-->Extensions**  tab as shown below:

![Gather Contacts Extension](https://github.com/clr2of8/GatherContacts/raw/master/images/AddExtension.png)

Click **Add-->SelectFile ...** and browse to the "GatherContacts.jar" file that you download from this repository.

## Step 3
Configure the Extension to save output to a file. This is where your usernames will be written. You can optionally select the "Show in UI" option, but the output window truncates items when the list gets too long.

![Save Output](https://github.com/clr2of8/GatherContacts/raw/master/images/outputFile.png)

## Step 4
Configure your browser to use Burp as a proxy as you normally would. From the browser, do a Google or Bing search of the following form (don't forget the "/in" on the end of "linkedin.com":

site:linkedin.com/in "Company Name"
site:xing.com/profile "Company Name"

![Example](https://github.com/clr2of8/GatherContacts/raw/master/images/example.png)

Each of the employee names in the search results will be written to the output file you specified, as a tab delimited list. You can click on additional pages of results to get more employee names written to the file.

![Results links](https://github.com/clr2of8/GatherContacts/raw/master/images/google.png)

## Step 5
You can gather a large list of employee names quickly and easily with this method. Try importing the list into Microsoft Excel where you can use formulas to turn employee names into the appropriate username format such as first initial followed by last name.

![Import to Excel](https://github.com/clr2of8/GatherContacts/raw/master/images/excel.png)

![Data in Excel](https://github.com/clr2of8/GatherContacts/raw/master/images/exampleOutput.png)

## Step 6
When you are done, unload the Extension so you don't burden Burp with inspecting all responses.

Note: If you aren't getting a name written to the output file as you expect, it could be that the name was already ouput by the extension since it was loaded. To reset everything, unload (uncheck) the extension and then reload it.

## Extra Info

For those of you not familiar with Excel formula's, here are some formulas for creating usernames and email addresses from the output above. (Assume column B contains the first name and column C contains the last name)

![Data in Excel](https://github.com/clr2of8/GatherContacts/raw/master/images/formulas.png)

## Pro Tips

Randomize the order of your username list before spraying to avoid being detected in some cases. You can add a column of random numbers to your spreadsheet using the **=RAND()** formula, then sort by this column.

Randomize your source IP using ProxyCannon from [#_shellIntel](https://www.shellntel.com/blog/2016/1/14/update-to-proxycannon) as described [here](https://www.blackhillsinfosec.com/using-burp-proxycannon/).


