# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.


#############################################################################################################
#############################################################################################################

After reading the entire document i have understood this system the following way:

    Server
----------------
			**				   						
Jan.csv			-------------------------							**	
Feb.csv			| Internal DataStructure |	    **					         ----------------------------- 
.		 ---->	| for Data processing	 | -------> Min , max , Count of breach , Trend --------> All the Data accumulated ,
.		 input	-------------------------   input	    Logic and solution.		 input	  seperated based on analysis
.													 -----------------------------	
.													             |
----------------												     |  input
			    **					Server						    \ /
   Notification	<------	    Notification		---------------------	**			------------------------------
     Interface	 input	    handling	 <-------	Jan_W1.PDF	       <------ PDF file <-----	Off the shelf / External vendor
					  input		Jan_W2.pdf		Store		output  provided PDF converter.
								.					------------------------------
								.
							---------------------

above that the "**" marked points are our Testable code.
Based on this understanding the following ans are provided.

#############################################################################################################
#############################################################################################################



Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
1. CSV to PDF export tool availability for automated generation.
1. Based on the notification type the interface access is required.

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | This is external interface. A fake function shall be used for testing.
Counting the breaches       | Yes           | part of the analysis reason. This is part of the software being developed
Detecting trends            | Yes 	    | part of the analysis reason. This is part of the software being developed
Notification utility        | No 	    | This is external interface. Shall be tested as Mock munction.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Storage of PDF files in the system with proper date and time.
4. Write "Battery x reading increasing everyday / <on perticular days> from time a-b" if certain trend is noticed.
5. Write battery no of breaches based on the battery threshold data cross in the CSV file.
6. Sending notification to the interface when PDF is available.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file 	  | Notification interface
				     	     (mail etc..)               | Mock Notification function
Report inaccessible server | server connection error	  | unable to fetch csv               | fake connection/sever not reachable code
Find minimum and maximum   | csv file | internal data-structure to update in PDF               | None - Pure fuction to find out min max.
Detect trend               | Csv file | update the trend in PDF               | None - Pure fuction to figure out trend.
Write to PDF               | Internal data structure | Converted PDF               | Fake - PDF cnverter.
