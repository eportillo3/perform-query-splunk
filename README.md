<h1>Perform a query with Splunk</h1>

<h2>Activity Overview</h2>

So far, you've learned that SIEM tools, such as Splunk, are an important part of a security analyst's toolbox because they provide a platform for storing, analyzing, and reporting on data from different sources. You also explored some basic searches using Splunk's querying language, called Search Processing Language (SPL), which included the use of pipes and wildcards.

Creating effective searches is an important skill because it enables you to quickly and accurately find the information you are looking for within a large amount of data. Quick and accurate searching is especially useful during incident response, because you might need to swiftly identify and address a security incident. Effective search techniques also help you efficiently identify patterns, trends, and anomalies within data.

<h2>Scenario</h2>

Review the following scenario. Then complete the step-by-step instructions.

You are a security analyst working at the e-commerce store Buttercup Games. You've been tasked with identifying whether there are any possible security issues with the mail server. To do so, you must explore any failed SSH logins for the root account. 

<h2>Activity walk-through:</h2>

<h3>Step 1: Access supporting materials</h3>

The following supporting materials will help you complete this activity. The data contains log and event information from Buttercup Games' mail servers and web accounts. This includes information like access and authentication logs, email logs, and more.


To download this data, click the link then click the download icon.

Link to supporting materials: <a href="https://drive.google.com/file/d/1nDz_DZB4ADbD4tvaDa54_l1FoT_jtVy4/view">tutorialdata.zip</a> 

<h3>Step 2: Create a Splunk Cloud account</h3>

To use Splunk Cloud, you must create an account. Follow Part 1 - Create a Splunk Cloud account and Part 2 - Verify your email

<h3>Step 3: Sign up for a free Splunk Cloud trail</h3>

After you've created your Splunk account, you'll need to sign up for a free Splunk Cloud trial. Follow Part 3 - Activate a Splunk Cloud trial

<h3>Step 4: Upload data into Splunk</h3>

To operate effectively, it's essential that SIEM tools ingest and index data. SIEM tools collect and process data so that it becomes searchable events that can be queried, viewed, and analyzed.

So far, you've created a Splunk account and activated and accessed the Splunk Cloud free trial, but your Splunk Cloud instance does not contain any data. Next, you'll need to upload data into Splunk to start querying. Complete the following steps to upload data into Splunk:

1. If you haven't already, download the data file from Step 1:  <a href="https://drive.google.com/file/d/1nDz_DZB4ADbD4tvaDa54_l1FoT_jtVy4/view">tutorialdata.zip</a> 
. Click the link then click the download icon. Do not uncompress the file.

2. Navigate to Splunk Home from your Splunk Cloud free trial instance. You might need to log in again using your credentials from Step 3.

3. On the Splunk bar, click Settings. Then click the Add Data icon.

4. Click Upload.

5. Click the Select File button.

6. Upload the tutorialdata.zip file, and click Open.

7. Click the Next button to continue to Input Settings.

8. By the Host section, select Segment in path and enter 1 as the segment number.

9. Click the Review button and review the details of the upload before you submit. The details should be as follows: 

Input Type: Uploaded File

File Name: tutorialdata.zip

Source Type: Automatic

Host: Source path segment number: 1 

Index: Default

10. Click Submit. Once Splunk has ingested the data, you will receive confirmation that the file was successfully uploaded.

<h3>Step 5: Perform a basic search</h3>

Take a moment to examine the Splunk Cloud interface by locating the app panel, the Explore Splunk panel, and the Splunk bar.

<img src="https://i.imgur.com/l8A5O0Z.png" height="80%" width="80%"/>

Now that you've uploaded the data into Splunk, perform your first query to confirm that the data has been ingested, indexed, and is searchable. Follow these steps to perform a query:

1. Navigate to Splunk Home. (To return to Splunk Home, click the Splunk Cloud logo on the Splunk Cloud page.)

2. Click Search & Reporting. You may close any pop ups that appear.

3. In the search bar,  enter your search query:
index="main"
This search term specifies the index. An index is a repository for data. Here, the index is a single dataset containing events from an index named main.

4. Select All Time from the time range dropdown to search for all the events across all time.

5. Click the search button. Note that the search button is represented by the magnifying glass icon. Your search should retrieve thousands of events.

<img src="https://i.imgur.com/8IFxrNx.png" height="80%" width="80%"/>

<h3>Step 6: Evaluate the fields</h3>

When Splunk indexes data, it attaches fields to each event. These fields become part of the searchable index event data. This helps security analysts easily search for and find the specific data they need. Now that you've run your first query, examine the search results and the fields.

For each event the fields are host, source, and sourcetype. Under SELECTED FIELDS, examine the same fields.

<img src="https://i.imgur.com/ocnuMmo.png" height="80%" width="80%"/>

Examine the field values by clicking on the field under SELECTED FIELDS. You should observe the following:

- host: The host field specifies the name of the network host from which the event originated. In this search there are five hosts:

  - mailsv - Buttercup Games' mail server. Examine events generated from this host.

  - www1 - This is one of Buttercup Games' web applications.

  - www2 - This is one of Buttercup Games' web applications.

  - www3 - This is one of Buttercup Games' web applications.

  - vendor_sales - Information about Buttercup Games' retail sales.

- source: The source field indicates the file name from which the event originates. You should identify eight sources. Notice /mailsv/secure.log, which is a log file that contains information related to authentication and authorization attempts on the mail server.

- sourcetype: The sourcetype determines how data is formatted. You should observe three sourcetypes. Examine secure-2.

<h3>Step 7: Narrow your search</h3>

Because you've been tasked with exploring any failed SSH logins for the root account on the mail server, you'll need to narrow the search results for events from the mail server.

Under SELECTED FIELDS, click host and click mailsv.

Notice that a new term has been added to the search bar: index=main host=mailsv. The search results have narrowed to over 9000 events that are generated by the mail server.

<img src="https://i.imgur.com/RR7NiJt.png" height="80%" width="80%"/>

<h3>Step 8: Search for a failed login for root</h3>

Now that you've narrowed your search results to events generated by the mail server, continue to narrow the search to locate any failed SSH logins for the root account. 

1. Clear the search bar.

2. Enter index=main host=mailsv fail* root into the search bar.
This search expands on the search from the previous task and searches for the keyword fail*. The wildcard tells Splunk to expand the search term to find other terms that contain the word fail such as failure, failed, etc. Lastly, the keyword root searches for any event that contains the term root.

3. Click search.

<img src="https://i.imgur.com/vJvfvN6.png" height="80%" width="80%"/>

<h3>Step 9: Evaluate the search results</h3>

Your search from the previous task should have retrieved search results for over 300 events. Navigate to other pages of the search results to observe the events not listed on the first page of results.

Pro tip: Splunk highlights search terms in search results to make it easier to identify where the search terms appear in the data.

<h2>Key takeaways</h2>

In this activity, you used Splunk Cloud to perform a search and investigation. Using Splunk Cloud, you were able to:

- Upload sample log data 

- Search through indexed data

- Evaluate search results

- Identify different data sources 

- Locate failed SSH login(s) for the root account
