# How to pass a JSON array to WinUI Chart (SfCartesianChart)?

JSON data cannot be bound directly to [SfCartesianChart](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html), so we should deserialize the JSON data to a bindable format. You can use the open source NuGet [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) to serialize and deserialize the JSON objects.

The following steps explain how to pass JSON data to [SfCartesianChart](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.SfCartesianChart.html).

**JSON data**

```
{
	'Country': 'USA',
	'Count': 46
}, {
	'Country': 'China',
	'Count': 36
}, {
	'Country': 'Japan',
	'Count': 63
}, {
	'Country': 'Australia',
	'Count': 54
}, {
	'Country': 'France',
	'Count': 50
}
```

**Step 1:** Add the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) reference in your project.

**Step 2:** Create a data model to store JSON data.

```
public class Medal
{
    public string Country { get; set; }
    public int Count { get; set; }
}
```

**Step 3:** Create a ViewModel to store a collection of model objects.

```
public class ViewModel
{
    public ObservableCollection<Medal> Medal { get; set; }
}
```

**Step 4:** Deserialize the JSON data as a collection of data models.

```
{
     …
     string jsonData = @"{'Medal':[{'Country':'USA','Count':46},{'Country':'China','Count':36},{'Country':'Japan','Count':63},{'Country':'Australia','Count':54},{'Country':'France','Count':50}]}";

     var jsonDataCollection = JsonConvert.DeserializeObject<ViewModel>(jsonData);
     chart.DataContext = jsonDataCollection;
}
```

**Step 5:** Bind the deserialized JSON data to the ChartSeries [ItemsSource](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.ChartSeries.html#Syncfusion_UI_Xaml_Charts_ChartSeries_ItemsSource) property and set the [XBindingPath](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.ChartSeriesBase.html#Syncfusion_UI_Xaml_Charts_ChartSeriesBase_XBindingPath) and [YBindingPath](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Charts.XyDataSeries.html?tabs=tabid-1#Syncfusion_UI_Xaml_Charts_XyDataSeries_YBindingPath) properties, so that chart would fetch values from the respective properties in the data model to plot the series.

```
<chart:SfCartesianChart x:Name="chart">
    …
    <chart:ColumnSeries ItemsSource="{Binding Medal}"
                        XBindingPath="Country" 
                        YBindingPath="Count">
    </chart:ColumnSeries>
</chart:SfCartesianChart>
```

## Output:

![WinUI column chart with JSON data](https://user-images.githubusercontent.com/53489303/199639335-7c8d3ebb-87e8-4861-aeab-4315804e5210.png)

KB article - [How to pass a JSON array to WinUI Chart (SfCartesianChart)?]()
