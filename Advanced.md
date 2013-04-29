Advanced
========

### Modifying Charts

There may be situations where you will want to modify your charts data or type without redrawing the whole dashboard. You may want to retrieve values a user sets
or you may want to trigger events or perform calculations based on these values. The jQuery plugin from FusionCharts covers these situations by providing you with 
very simple API for these tasks. 

*  updateFusionCharts(updateConfigurations : Object) 
   Provides an implementation where you can pass new parameters and modify base configuration(height,width,datasource) of an existing chart.

*  attrFusionCharts(chartAttribute : string) 
   It is used to modify the cosmetic properties of the chart like captions, colors etc. 

*  cloneFusionCharts(callback:function, [cloneConfigurations : Object]) 
   Returns a new chart object , useful when you want to change data and values without disturbing the original, and passes it to the specified callback
   function.

#### updateFusionCharts(updateConfigurations : Object) 

This method helps in updating chart configurations of an existing chart at run-time. You can re-configure swfUrl, dataSource, dataFormat, width, height,
renderer, bgColor, debugMode, scaleMode etc. of existing charts. The syntax for using the update method with a container is.

        $(“.selector”).updateFusionCharts (updateConfigurations: Object);


__Examples__

Suppose we need to change the data source and type of a chart that is already rendered we can use 

      $("#chartContainer").updateFusionCharts( {"dataSource": file, "dataFormat": "xml""})

Or change the type of the chart from something to a 3D Column chart

      $("#chartContainer").updateFusionCharts( {"swfUrl" : "MSColumn3D.swf"})

#### attrFusionCharts(chartAttribute : string) 

This function can be used when one wants to change the chart titles, theme colors, number formatting or scaling setup,
divisional line and grid configurations and other cosmetic features of existing charts.The syntax for using
the attrFusionCharts method with a chart is


    $(“.selector”).attrFusionCharts( chartAttribute : string)

This function is overloaded to help get and set attribute values on the fly and search within objects.

    $(“.selector”).attrFusionCharts( chartAttribute:string, newValue:string)
    $(“.selector”).attrFusionCharts( chartAttributes : Object)

The first function call finds all the charts rendered in the selected elements and retrieves the value of a chart parameter from those charts or 
updates those charts with new parameter values. If a value is passed as a second parameter (newValue) to the method along with the name of 
the chart attribute through chartAttribute (as first parameter), the chart gets updated with the new parameter value.


__Examples__

You can change the captions on existing charts like this 

    $("#chartContainer" ).attrFusionCharts( "caption", "New Sales Data" )

Or change the theme of the chart dynamically like this 

    $("#chartContainer" ).attrFusionCharts( {"palette": "5", "paletteColors": "D977B7"})

#### cloneFusionCharts(callback:function, [cloneConfigurations : Object])

This method makes copy of either one or more charts and passes the list of cloned chart objects to a function for
further processing. The method looks for all the charts from the jQuery selector and clones them. 
An array of cloned chart objects is passed to a callback function whose name or reference needs to be passed as a 
mandatory parameter to cloneFusionCharts method. One can also use an anonymous function as the callback function. 
The general syntax is 

    $("#chartContainer" ).cloneFusionCharts(callback:function, [cloneConfigurations : Object])

__Examples__

You can clone a chart from one container into another one using code like this

    $("#leftPanel").cloneFusionCharts( function() { 
        $("#rightPanel").insertFusionCharts(this[0]); }, { renderer: "javascript" 
    } );

Or you can pass a smaller version of a chart to a backend application using a callback like this


    $(“#chartContainer”).cloneFusionCharts(callbackFn, {width:300, height: 400})
    
###Selectors 

Fusion Charts for jQuery has a selector that helps developers in selecting specific charts from within the dashboard. One can use the :FusionCharts selector like any standard jQuery selector component to traverse through the dashboard looking for charts. This is a powerful tool when working on a dashboard that has many individual components and you have to make changes on specific components. The general syntax for using selectors is 

    $(".selector :FusionCharts").function({}) ;

__Use Cases__

Suppose you want to change the background color on only the 4th chart in your dashboard

    $("<html> :FusionCharts").eq(‘3’).attrFusionCharts( {bgColor : "ecdecd"})

Or change captions on any of the Chart components in the page body. 

    $("<body>").find(":FusionCharts")
    {
    this.attrFusionCharts( {caption: "New Caption Set"})
    }

Maybe set that caption only to the 1st Chart 

    $("<body> :FusionCharts").eq(0).attrFusionCharts( {caption: "New Caption Set"})

Or destroy all the chart instances in a given container

    $("<body>").find(":FusionCharts")
    {
    this.dispose();
    }

For a detailed API reference on the :FusionCharts selector click [here](http://docs.fusioncharts.com/charts/).

### Events

FusionCharts for jQuery taps into the event model available with jQuery, which means when an event is triggered, you can catch such events either at a component level or all the way up at the root of the DOM tree. Almost every step of the chart creation process triggers events, you can listen for anything specific and write callbacks only for these events. 

FusionCharts jQuery plugin also enables you to bind FusionCharts events using jQuery bind method. The event handler needs to be attached to the the container element of the FusionCharts object. To avoid conflict with other jQuery events having same names, "fusioncharts" has been appended to all the FusionCharts event names or types.

The syntax to bind to an event is 

        $(".selector").bind( "Event", function (e, args) { });

Events in FusionCharts are categorized into two broad groups - Simple Events and Advanced events. Each event provides arguments to the event-listeners. In the simple event model , most of events (except for `FC_Exported and FC_Resized` events) provide the DOMId of the source chart that raised the event.  In the advanced model, two event parameters are passed to the event listener function. The first parameter, eventObject, is structurally common for all events. The second parameter, argumentsObject contains event specific properties like 

1.  The first argument is eventObject which provides details of the event. It is an object which provides three properties :
  *  eventId : An unique ID given to the event
  *  eventType : A String containing the name or the event type, for example, "rendered" etc.
  *  sender : A FusionCharts JavaScript Object reference to the chart which has raised that event  

2. The second argument argumentsObject is an Object which contains details of the particular event fired. As per the type of the event the properties of parameter   object varies

For a complete reference of the Events API click [here](http://docs.fusioncharts.com/charts/contents/JavaScript/API/Events.html).

__Examples__

To listen to the DrawComplete event and display an alert.
    
    $("#chartContainer").bind( "fusionchartsdrawcomplete", function (e, args) { 
     alert("Chart named " + e.sender.id + " has completed chart drawing." ); 
    }); 

To display a chart only after it has rendered 

    $("#chartContainer").bind( "FC_Rendered", function (e, args) { 
     this.show(); 
    });   

To know if a chart is ready for print 

    $("#chartContainer").bind( "fusionchartsPrintReadyStateChange", function (e, args)
    {     some code ;     });   

### Namespace Conflicts




