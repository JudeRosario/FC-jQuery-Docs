The Basics
==========

Download and Setup 
------------------

Download the latest version of the FusionCharts for jQuery Plug-in from [here](http://www.fusioncharts.com/jquery/), it also is included with the FusionCharts Suite XT 

package. Copy and paste the required files in your web directory
.
 Yow will need these 3 files specifically to be served with permissions set correctly. 

1. FusionCharts.js.
2. HTMLTableDataHandler.
3. FusionCharts.jQueryPlugin.js.

Once thats done, include the 3 files in any web page/app you want charts to be displayed on, you can also copy / paste the code below in the header section of your 

page.
                <script type="text/javascript" src="path/to/FusionCharts.js"></script>
  	<script type="text/javascript" src="path/to/FusionCharts.HTMLTableDataHandler.js"></script>
		<script type="text/javascript" src="path/to/FusionCharts.jQueryPlugin.js"></script>

Skip this section if you already have jQuery set-up. It is highly __recommended__ that you use it from a CDN, it is highly secure and many of your users already have 

the file in cache. Copy paste the code below to always fetch the latest minified version of jQuery from their CDN . 

            <script type="text/javascript" src="http://code.jquery.com/jquery-latest.min.js></script>

Alternatively you can host and serve jQuery yourself, download it from [here](http://jquery.com/download/) and copy paste into your web directory before using it 

exactly as above.

Setting up the DataSource
-------------------------

The jQuery plug-in comes with a initialising function inserttoFusionCharts(args1[] , args2[]) , we will come to the arguments part shortly , this function is 

responsible for creating chart components and rendering them at a given container on the screen. This is what most of you ever will need for your basic charting needs. 

###Charts from XML Data

You will need either a validated XML which contains the data needed to draw your chart. Keep in mind that every node in this xml file must convey some information 

about your chart. Here is how a sample XML file would look for a simple 3D Bar Chart. The whole chart must exist within &lt;chart&gt;tags.

	<chart caption='Weekly Sales Summary'
   	xAxisName='Week' yAxisName='Sales' numberPrefix='$'> 
    	<set label='Week 1' value='14400' /> 
    	<set label='Week 2' value='19600' /> 
    	<set label='Week 3' value='24000' /> 
    	<set label='Week 4' value='15700' /> 
	</chart>

Now suppose you had this file saved on your webserver as sales.xml, This is how we create and add the chart to a container.

	$(document).ready(function(){
               $("#chartContainer").insertFusionCharts({
               swfUrl: "FusionCharts/Column3D.swf", 
               dataSource: "/path/to/sales.xml", 
               dataFormat: "xmlurl", 
               renderer: “javascript”
         });

Alternately, you can have hard coded XML and directly pass it to the function like this 

	$("#chartContainer").insertFusionCharts({
               swfUrl: "FusionCharts/Column3D.swf", 
               renderer: "JavaScript",
               width: "400", 
               height: "300", 
               id: "myChartId",
	       renderer: “javascript”

               dataFormat: "xml", 
               dataSource: "<chart caption='Weekly Sales Summary' xAxisName='Week' " +
                 "yAxisName='Sales' numberPrefix='$'>" +
                 "<set label='Week 1' value='14400' />" +
                 "<set label='Week 2' value='19600' />" +
                 "<set label='Week 3' value='24000' />" +
                 "<set label='Week 4' value='15700' />" +
                 "</chart>"
         });

Both of them produce the same output , you can use the second option when creating basic charts with very little data.

###Charts from JSON Objects/Strings

If you had the same data as a JSON string inside sales.json like this, for more information about JSON itself and how to fomat it for Fusion Charts click [here]

(http://docs.fusioncharts.com/charts/contents/DataFormats/JSON/Overview.html)

{ 
    "chart": { 
          "caption" : "Weekly Sales Summary" ,
          "xAxisName" : "Week",
          "yAxisName" : "Sales",
          "numberPrefix" : "$"
    },
        
    "data" : 
     [
          { "label" : "Week 1", "value" : "14400" },
          { "label" : "Week 2", "value" : "19600" },
          { "label" : "Week 3", "value" : "24000" },
          { "label" : "Week 4", "value" : "15700" }
     ]
}

You can call the insertFusionCharts Function with slightly different parameters this way

	$(document).ready(function(){
               $("#chartContainer").insertFusionCharts({
               swfUrl: "FusionCharts/Column3D.swf", 
               dataSource: "/path/to/sales.json", 
               dataFormat: "jsonurl", 
               renderer: “javascript”
         });

Similarly you can copy paste a hard-coded JSON HTML strings to this function.

	$("#chartContainer").insertFusionCharts({
               swfUrl: "FusionCharts/Column3D.swf", 
               renderer: "JavaScript",
               width: "400", 
               height: "300", 
               id: "myChartId",
	       renderer: “javascript”

               dataFormat: "xml", 
               dataSource: 	{ 
        "chart": 
        { 
                "caption" : "Weekly Sales Summary" ,    
                "xAxisName" : "Week", 
                "yAxisName" : "Sales",  
                "numberPrefix" : "$" 
        },

        "data" : 
        [ 
                { "label" : "Week 1", "value" : "14400" },
                { "label" : "Week 2", "value" : "19600" }, 
                { "label" : "Week 3", "value" : "24000" }, 
                { "label" : "Week 4", "value" : "15700" } 
        ]
				}
	});

For a complete API reference of the insertfusioncharts() function click here

### Charts from HTML Tables

You can now directly take data from your HTML tables and convert it into a stunning chart. Your table must use standard html markup tags (<th>,<td>,<tr> etc), the FC 

jQuery engine can even validate unevenly spaced rows/columns using the span attribute.

The general syntax to convert a table to a chart is 


	$(".selector").convertToFusionCharts(chartOptions[], convertOptions[]);

chartOptions is an array that you pass, which defines the charts configuration, in terms of some key metics like those shown below, there are other chartOptions like 

lang, bgcolor, debug mode for a complete list click [here](http://docs.fusioncharts.com/charts/).

*Type
*Data format 
*Height and Width
*Renderer 

convertOptions is the second array which tells the chart how exactly to interpret the data it gets from the table. The main parameters here are

*Chart Attributes
  *Caption
  *X Axis / Y Axis Names
*Major
*Label Options
*Legend Options

It’s that simple,this one function takes all the options needed to parameterize your chart and returns a chart object.  for a complete reference of chartOptions and 

convertOptions and the API Reference of convertToFusioncharts click [here](http://docs.fusioncharts.com/charts/).


Now let us convert a simple table that looks like this into a chart, the HTML code of the table would look like this,

	<table id="dataTable">
				<tbody><tr>
					<th></th>
					<th class="center-align">2012</th>
					<th class="center-align">2013</th>
				</tr>
				<tr>
					<td>January</td>
					<td class="center-align">400</td>
					<td class="center-align">800</td>
				</tr>
				<tr>
					<td>February</td>
					<td class="center-align">600</td>
					<td class="center-align">320</td>
				</tr>
				<tr>
					<td>March</td>
					<td class="center-align">540</td>
					<td class="center-align">740</td>
				</tr>
				<tr>
					<td>April</td>
					<td class="center-align">430</td>
					<td class="center-align">650</td>
				</tr>
				<tr>
					<td>May</td>
					<td class="center-align">350</td>
					<td class="center-align">650</td>
				</tr>
				<tr>
					<td>June</td>
					<td class="center-align">420</td>
					<td class="center-align">750</td>
				</tr>
				<tr>
					<td>July</td>
					<td class="center-align">430</td>
					<td class="center-align">760</td>
				</tr>
				<tr>
					<td>August</td>
					<td class="center-align">490</td>
					<td class="center-align">550</td>
				</tr>
				<tr>
					<td>September</td>
					<td class="center-align">480</td>
					<td class="center-align">640</td>
				</tr>
				<tr>
					<td>October</td>
					<td class="center-align">450</td>
					<td class="center-align">650</td>
				</tr>
				<tr>
					<td>November</td>
					<td class="center-align">440</td>
					<td class="center-align">640</td>
				</tr>
				<tr>
					<td>December</td>
					<td class="center-align">600</td>
					<td class="center-align">820</td>
				</tr>
			</tbody></table>

This table shows the sales of a product over the last 2 years broken down month wise, we can directly draw a chart component by calling the convertToFusionCharts() 

function like this 

$("#dataTable").convertToFusionCharts({
type: "mscolumn2d",
	width: "800",
	height: "300",
	dataFormat: "htmltable",
	renderAt:"chartContainer",
	renderer:"javascript"					
}, {"chartAttributes":{	caption:"Units sold in the last 2 years",
			xAxisName:"Month",
			yAxisName:"Units",
			bgColor:"FFFFFF" },
			 });


The chart output will look like this, observe just by changing the major attribute to ‘column’ we completely transform the output of our chart. Try it out.

Remember it is possible to draw from HTML elements that are not yet added to the DOM, these charts however become visible only after the created elements are added to 

the DOM.  
