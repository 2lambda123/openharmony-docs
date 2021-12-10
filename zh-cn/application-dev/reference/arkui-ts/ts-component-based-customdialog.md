# @CustomDialog<a name="ZH-CN_TOPIC_0000001192355895"></a>

**@CustomDialog**装饰器用于装饰自定义弹窗。

```
// custom-dialog-demo.ets
@CustomDialog
struct DialogExample {
    controller: CustomDialogController;
    action: () => void;

    build() {
        Row() {
            Button ("Close CustomDialog")
                .onClick(() => {
                    this.controller.close();
                    this.action();
                })
        }.padding(20)
    }
}

@Entry
@Component
struct CustomDialogUser {
    dialogController : CustomDialogController = new CustomDialogController({
        builder: DialogExample({action: this.onAccept}),
        cancel: this.existApp,
        autoCancel: true
    });

    onAccept() {
        console.log("onAccept");
    }
    existApp() {
        console.log("Cancel dialog!");
    }

    build() {
        Column() {
            Button("Click to open Dialog")
                .onClick(() => {
                    this.dialogController.open()
                })
        }
    }
}
```

