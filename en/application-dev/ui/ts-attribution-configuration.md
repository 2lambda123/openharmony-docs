# Attribution Configuration<a name="EN-US_TOPIC_0000001157228865"></a>

Use attribute methods to configure component attributes. An attribute method follows the corresponding component and is bound to the component using the "**.**" operator.

The following is an example of configuring the  **fontsize**  attribute of the  **<Text\>**  component:

```
Text('123')
    .fontSize(12)
```

You can also use the "**.**" operation to implement chain call to configure multiple attributes at the same time.

Below is the sample code for configuring the  **width**  and  **height**  attributes of the  **<Image\>**  component at the same time:

```
Image('a.jpg')
    .alt('error.jpg')
    .width(100)
    .height(100)
```

In addition to constants, you can also pass variables or expressions, as shown below:

```
// Size, count, and offset are private variables defined in the component.
Text('hello')
    .fontSize(this.size)
Image('a.jpg')
    .width(this.count % 2 === 0 ? 100 : 200)
    .height(this.offset + 100)
```

For attributes of preset components, the framework also provides some predefined enumeration types, which you can pass as parameters to methods.

Enumeration types must meet the parameter type requirements on the enumeration type definitions for specific attributes.

You can configure the font color and weight attributes of the  **<Text\>**  component as follows:

```
Text('hello')
    .fontSize(20)
    .fontColor(Color.Red)
    .fontWeight(FontWeight.Bold)
```

