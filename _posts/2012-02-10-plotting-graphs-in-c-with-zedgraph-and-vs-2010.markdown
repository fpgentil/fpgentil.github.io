---
title:  "Plotting graphs in C# with ZedGraph and VS 2010"
date:   2012-02-10 08:00:00
description:
---

About ZedGraph:

```
“ZedGraph is a class library, user control, and web control for .net, written in C#, for drawing 2D Line, Bar, and Pie Charts. It features full, detailed customization capabilities, but most options have defaults for ease of use.”
```

So, let’s get some code done!

1) Download ZedGraph, create your project and paste “ZedGraph.dll” into your project’s folder.

![zedgraph1](/assets/images/zedgraph/zedgraph1.png)

2) Now you must add ZedGraph as Reference in your project.

![zedgraph2](/assets/images/zedgraph/zedgraph2.png)

![zedgraph3](/assets/images/zedgraph/zedgraph3.png)

3) Then, open up your ToolBox and add ZedGraph there so this will let you drag and drop it.

![zedgraph4](/assets/images/zedgraph/zedgraph4.png)

![zedgraph5](/assets/images/zedgraph/zedgraph5.png)

4) Alright, so now drag and drop ZedGraph into your form. Probably you have something like this now:

![zedgraph6](/assets/images/zedgraph/zedgraph6.png)

Since this is just a tutorial, I’m going to make some random plots, trying to approach you to ZedGraph’s magic Smiley mostrando a língua.

5) Add the line below to your code.

```
using ZedGraph;
```

```
// pane used to draw your chart
GraphPane myPane = new GraphPane();

// poing pair lists
PointPairList listPointsOne = new PointPairList();
PointPairList listPointsTwo = new PointPairList();

// line item
LineItem myCurveOne;
LineItem myCurveTwo;
```

```
private void Form1_Load(object sender, EventArgs e)
{
    // set your pane
    myPane = zedGraphControl1.GraphPane;

    // set a title
    myPane.Title.Text = "This is an example!";

    // set X and Y axis titles
    myPane.XAxis.Title.Text = "X Axis";
    myPane.YAxis.Title.Text = "Y Axis";

    // ---- CURVE ONE ----
    // draw a sin curve
    for (int i = 0; i < 100; i++)
    {
        listPointsOne.Add(i, Math.Sin(i));
    }

    // set lineitem to list of points
    myCurveOne = myPane.AddCurve(null, listPointsOne, Color.Black, SymbolType.Circle);    
    // ---------------------

    // ---- CURVE TWO ----
    listPointsTwo.Add(10, 50);
    listPointsTwo.Add(50, 50);            

    // set lineitem to list of points
    myCurveTwo = myPane.AddCurve(null, listPointsTwo, Color.Blue, SymbolType.None);
    myCurveTwo.Line.Width = 5;
    // ---------------------

    // draw
    zedGraphControl1.AxisChange();              
}
```

PS: If you are working with a large mount of data and perhaps more than one thread, I highly recommend you to use ZedGraph. In this case, instead of using the method:

```
// draw
zedGraphControl1.AxisChange();
```

You can use the delegate below:

```
delegate void axisChangeZedGraphCallBack(ZedGraphControl zg);
private void axisChangeZedGraph(ZedGraphControl zg)
{
    if (zg.InvokeRequired)
    {
        axisChangeZedGraphCallBack ad = new axisChangeZedGraphCallBack(axisChangeZedGraph);
        zg.Invoke(ad, new object[] { zg });
    }
    else
    {               
        zg.AxisChange();
        zg.Invalidate();
        zg.Refresh();                
    }
}
```

And the result should be...

![zedgraph7](/assets/images/zedgraph/zedgraph7.png)

Thanks :)
