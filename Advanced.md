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

This function is overloaded to help get and set attribute values on the fly

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

__Examlples__

You can clone a chart from one container into another one using code like this

    $("#leftPanel").cloneFusionCharts( function() { 
        $("#rightPanel").insertFusionCharts(this[0]); }, { renderer: "javascript" 
    } );

Or you can pass a smaller version of a chart to a backend application using a callback like this


    $(“#chartContainer”).cloneFusionCharts(callbackFn, {width:300, height: 400})
