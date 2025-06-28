Hello everyone, welcome back to the special session on HarmonyOS 5 Meichuang chart components. Many of you may wonder what each property in different chart types does and how to use them. So, we'll explain each property in detail. Let's learn together!  

In this episode, we'll focus on the detailed usage of the `title` property in the McLineChart component. This property controls the display of the chart title, including rich configurations such as the style, position, and animation of the main and subtitle. Below, we'll deeply analyze each property and provide complete code examples.  


### 1. `show` Property  
**Function**: Controls whether the title is displayed.  
**Type**: Boolean  
**Default**: `true`  
**Options**: `true` | `false`  
**Scenario**: Use when dynamically toggling the title display.  
```typescript
title: { show: false } // Hide the title
```  


### 2. `text` Property  
**Function**: Sets the main title text content.  
**Type**: String  
**Default**: `''` (empty string)  
**Scenario**: Displays the core description of the chart.  
```typescript
title: { text: '2023 Sales Trend' } // Main title content
```  


### 3. `subtext` Property  
**Function**: Sets the subtitle text content.  
**Type**: String  
**Default**: `''` (empty string)  
**Scenario**: Provides supplementary information or data unit labels.  
```typescript
title: { subtext: 'Unit: 10,000 yuan' } // Subtitle content
```  


### 4. `direction` Property  
**Function**: Controls the arrangement direction of the main and subtitle.  
**Type**: String  
**Default**: `'column'` (vertical arrangement)  
**Options**: `'column'` | `'row'`  
**Scenario**: Use when displaying the main and subtitle horizontally side by side.  
```typescript
title: { direction: 'row' } // Horizontal arrangement
```  


### 5. `itemGap` Property  
**Function**: Sets the spacing between the main and subtitle.  
**Type**: Number  
**Default**: `5`  
**Scenario**: Adjusts the compactness between titles.  
```typescript
title: { itemGap: 10 } // Increase spacing
```  


### 6. Position Control Properties  
Includes four sub-properties: `left`, `right`, `top`, `bottom`:  
- **Function**: Controls the positioning of the title container.  
- **Type**: String | Number  
- **Default**: `'auto'`  
- **Example Values**: `'10%'` | `20` (pixel value)  
- **Scenario**: Use when precise title positioning is required.  
```typescript
title: { 
  left: '20%',  // 20% from the left
  top: 10       // 10 pixels from the top
}
```  


### 7. `offset` Property  
**Function**: Sets the pixel offset of the title.  
**Type**: Array  
**Default**: `[0, -20]`  
**Format**: `[horizontal offset, vertical offset]`  
**Scenario**: Fine-tunes the title position.  
```typescript
title: { offset: [10, 30] } // 10px right, 30px down
```  


### 8. `textStyle` Property (Object)  
Controls the main title text style with the following sub-properties:  
- **color**: Text color (String, default `'#333'`).  
- **fontSize**: Font size (Number, default `36`).  
- **fontWeight**: Font weight (String, default `'bold'`).  
- **fontFamily**: Font family (String, default `'sans-serif'`).  
- **textAlign**: Horizontal alignment (String, default `'center'`).  
- **textBaseline**: Vertical alignment (String, default `'bottom'`).  
```typescript
title: { 
  textStyle: { 
    color: '#1890FF', 
    fontSize: 24, 
    fontWeight: 'normal' 
  } 
}
```  


### 9. `subtextStyle` Property (Object)  
Controls the subtitle text style. Sub-properties are the same as `textStyle`, with differences:  
- **color** default: `'red'`  
- **fontSize** default: `28`  
- **fontWeight** default: `'400'`  
```typescript
title: { 
  subtextStyle: { 
    color: '#666', 
    fontSize: 16 
  } 
}
```  


### 10. `rLevel` Property  
**Function**: Sets the rendering level.  
**Type**: Number  
**Default**: `20`  
**Scenario**: Controls the overlay relationship between the title and other elements.  
```typescript
title: { rLevel: 100 } // Increase rendering level
```  


### 11. `animationCurve` Property  
**Function**: Sets the title display animation curve.  
**Type**: String  
**Default**: `'easeOutCubic'`  
**Options**: All CSS animation curve values.  
```typescript
title: { animationCurve: 'linear' } // Linear animation
```  


### 12. `animationFrame` Property  
**Function**: Sets the animation frame count.  
**Type**: Number  
**Default**: `30`  
**Special Value**: `0` disables animation.  
```typescript
title: { animationFrame: 50 } // Smoother animation
```  


### Comprehensive Application Example  
Now that we've covered each property's function, type, default value, options, and scenarios, let's see a comprehensive example:  

```typescript
import { McLineChart, Options } from '@mcui/mccharts'

@Entry
@Component
struct Index {
  @State maxData: number[] = [11, 11, 15, 13, 12, 130, 10] // Initialize data
  
  @State seriesOption: Options = new Options({
    title: {
      show: true,
      text: 'Temperature Data',
      subtext: 'Jan-Apr 2023',
      direction: 'row',
      itemGap: 15,
      left: 'center',
      top: 20,
      textStyle: {
        color: '#1E88E5',
        fontSize: 28,
        fontFamily: 'Microsoft YaHei'
      },
      subtextStyle: {
        color: '#757575',
        fontSize: 16
      },
      animationCurve: 'easeInOutBack'
    },
    xAxis: {
      data: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
    },
    series: [{
      name: 'Maximum Temperature',
      data: this.maxData
    }]
  })

  // Dynamically modify data
  aboutToAppear() {
    setTimeout(() => {
      // Pass properties to modify (no need to pass all)
    }, 2000)
  }

  build() {
    Row() {
      McLineChart({
        options: this.seriesOption
      })
    }
    .height('50%')
  }
}
```  


### Practical Scenario Extension  
In an e-commerce data dashboard, dynamically update `title.text`:  

```typescript
// Update title based on filtering conditions
function updateTitle(month: string) {
  // Update data source
  this.maxData = [110, 110, 150, 130, 120, 190, 100];
  this.minData = [-1, -2, -2, -5, 3, -2, 0];

  // Dynamically configure the chart
  this.seriesOption.setVal({
    title: {
      text: `${month} Month Temperature Data`,  // Dynamically bind month to main title
      subtext: `Year-on-Year ${data.growthRate}%`  // Show growth rate in subtitle
    },
    series: [
      { 
        name: 'Maximum Temperature', 
        data: this.maxData  // Bind maximum temperature data
      },
      { 
        name: 'Minimum Temperature', 
        data: this.minData   // Bind minimum temperature data
      }
    ]
  });
}
```  


That's all for this episode. We hope this article helps you fully master the usage of the McLineChart title component. Apply these properties flexibly in your development to create professional-grade data visualizations. See you next time!
