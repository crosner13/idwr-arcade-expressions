# Flow indicator widget

This widget was originally created for use in the Trust Water Rights dashboard. It reads the attributes
of a dynamic flow gauge service provided by Esri Livefeeds and styles an indicator widget based on a range of values. 

## Use case

This is designed specifically for Dashboards that use Indicator widgets to show values that could fall along a qualitative spectrum.
In this example, we are displaying flow at certain points in our map and changing the widget appearance depending on the flow value. 

Out of the box, Indicator widgets only show one color on either side of a defined threshold. This custom expression is a workaround for that limitation.
The logic outlined in the expression template below can be applied to other widgets that display values you would like to showcase similarly. 

## Workflow 

After enabling Advanced formatting in Indicator options, copy and paste the expression found in the template below to the expression box. 

To configure the widget to your layer, you must provide a field name for your data point that contains a numerical value. The expression can be
further configured to have more descriptors if they are added to the `flowQuality` variable or the dictionary `flowIndicatorDict`. 


```js
var flow = $datapoint["YOUR_FIELD_NAME_HERE"]

var winterMonths = [1,2,12];

var currentMonth = ISOMonth(Date())

if (Includes(winterMonths, currentMonth) == true) {
    var flowQuality = When(
    flow <= 5600, "Very Low",
    flow > 5600 && flow <= 7800, "Low",
    flow > 7800 && flow <= 11700, "Moderate",
    flow > 11700 && flow <= 15600, "High",
    flow > 15600, "Very High",
    "Flow rate unavailable.");
} else {
    var flowQuality = When(
    flow <= 3900, "Very Low",
    flow > 3900 && flow <= 7800, "Low",
    flow > 7800 && flow <= 11700, "Moderate",
    flow > 11700 && flow <= 15600, "High",
    flow > 15600, "Very High",
    "Flow rate unavailable.");
}

var flowIndicatorDict = {
	"Very Low": {
		"color":'#D7191C',
		"textColor":"#FFFFFF",
		"bottomText":"Very Low - Trust Water Rights are Curtailed",
		"iconName":"alert",
		"iconAlign": "left",
	},
	"Low": {
		"color":"#FDAE61",
		"textColor":"#000000",
		"bottomText":"Low",
		"iconName":"",
		"iconAlign": "",
	},
	"Moderate": {
		"color":"#FFFFBF",
		"textColor":"#000000",
		"bottomText":"Moderate",
		"iconName":"",
		"iconAlign": "",
	},
	"High": {
		"color":"#A6D96A",
		"textColor":"#000000",
		"bottomText":"High",
		"iconName":"",
		"iconAlign": "",
	},
	"Very High": {
		"color":"#1A9641",
		"textColor":"#FFFFFF",
		"bottomText":"Very High",
		"iconName":"",
		"iconAlign":"",
	},
}

var flowDisplay = flowIndicatorDict[flowQuality]

var color = flowDisplay.color

var textColor = flowDisplay.textColor

var flowQualText = flowDisplay.bottomText

var icon = flowDisplay.iconName

var iconPosition = flowDisplay.iconAlign

return {
    textColor: textColor,
    backgroundColor: color,
    topText: 'Flow at Swan Falls Dam',
    topTextColor: '',
    topTextOutlineColor: '',
    topTextMaxSize: 'medium',
    middleText: flow + " cfs",
    middleTextColor: textColor,
    middleTextOutlineColor: '',
    middleTextMaxSize: 'large',
    bottomText: flowQualText,
    bottomTextColor: textColor,
    //bottomTextOutlineColor: '',
    bottomTextMaxSize: 'medium',
    iconName: icon,
    iconAlign: iconPosition,
    iconColor: textColor,
    //iconOutlineColor:'',
    //noValue:false,
    //attributes: {
      // attribute1: '',
      // attribute2: ''
    // }
  }
```
The `icon` is configured in the Indicator options, outside of Advanced formatting. 
