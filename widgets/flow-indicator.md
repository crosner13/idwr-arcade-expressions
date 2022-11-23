# Flow indicator widget

This widget was originally created for use in the Trust Water Rights dashboard. It reads the attributes
of a dynamic flow gauge service provided by Esri Livefeeds. 

```js
var flow = $datapoint["flow_cfs"]

var flowQuality = When(
    flow <= 3900, "Very Low",
    flow > 3900 && flow <= 7800, "Low",
    flow > 7800 && flow <= 11700, "Moderate",
    flow > 11700 && flow <= 15600, "High",
    flow > 15600, "Very High",
    "Flow rate unavailable.")

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

