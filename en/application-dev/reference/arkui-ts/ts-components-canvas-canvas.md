# Canvas


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE：**
> This component is supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


The **&lt;Canvas&gt;** component can be used to customize drawings.


## Required Permissions

None


## Child Components

None


## APIs

Canvas(context: CanvasRenderingContext2D)

- Parameters
    | Name | Type | Mandatory | Default&nbsp;Value | Description |
  | -------- | -------- | -------- | -------- | -------- |
  | context | [CanvasRenderingContext2D](ts-canvasrenderingcontext2d.md) | Yes | - | For&nbsp;details,&nbsp;see&nbsp;CanvasRenderingContext2D. |


## Attributes

[Universal attributes](ts-universal-attributes-size.md) are supported.


## Events

In addition to [universal events](ts-universal-events-click.md), the following events are supported.

  | Name | Parameter | Description | 
| -------- | -------- | -------- |
| onReady(callback:&nbsp;()&nbsp;=&gt;&nbsp;void) | None | Triggered&nbsp;when&nbsp;. | 


## Example


```
@Entry
@Component
struct CanvasExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.context.fillRect(0,30,100,100)
        })
    }
    .width('100%')
    .height('100%')
  }
}
```
