# Orange-Basic

目前开源UI弹窗组件


## 一、UI组件：orangedialog

> 前言

> OrangeDialog组件使用Builder模式构建，设计上参考Android系统的AlertDialog，具有很强的扩展性。

> orangeframe库中的PushDialog是基于DialogFragment构建的，因此将PushDialog重构为FMDialog

### 使用方式

```
implementation 'com.zhidiantech:orangedialog:1.0.0'
```

### 兼容性
- 基于v4包下的DialogFragment,可兼容低版本
- 组件化Android 版本 >=21

### 能力
- 支持自定义弹窗实现
- 支持自定义弹窗动画
- 支持弹窗百分比设置宽高
- 支持弹窗显示在任意位置 FMDialog.GRACITY_LOCATION
- 支持处理弹窗内View
- 支持弹窗内View状态的保存与恢复
- 支持点击阴影关闭弹窗

### 普通创建FMDialog

``` 
 //实例化Builder
 FMDialogBuilder fmDialogBuilder=new FMDialogBuilder();
 //Build弹窗样式
 fmDialogBuilder.setFragmentManager(getSupportFragmentManager())
                .setAnimRes(0)
                .setGravity(FMDialog.GRAVITY_TOP)
                .setHeightPercent(0.5f)
                .setWidthPercent(1f)
                .setIsCancel(true)
                .setLayoutRes(R.layout.dialog_sample)
                .setSaveState(false);
 //动态实例化弹窗
 FMDialog fmDialog=fmDialogBuilder.createDialog();
 
 ```
 
### 自定义弹窗

1.在设计低层的抽象时，考虑到弹窗具有的几个重要特性，在DialogBuilder中向高层抛出了几个关键方法

2.在DialogPower中定义了构建弹窗时所需的参数Key,这么做是为了避免（魔法参数-来自EffectiveJava一书）的出现，

例如,在赋值时，可以使用DialogPower.LAYOUTRES 等

```

 //创建自己的Builder ，继承自DialogBuilder
 //DialogBuilder接受一个泛型，可指定自定义的弹窗 如CustomDialog

public class CustomDialogBuilder extends DialogBuilder<CustomDialog> {

    @Override
    public DialogBuilder setLayoutRes(int layoutRes) {
        return this;
    }

    @Override
    public DialogBuilder setWidthPercent(float widthP) {
        return this;
    }

    @Override
    public DialogBuilder setHeightPercent(float heightP) {
        return this;
    }

    @Override
    public DialogBuilder setIsCancel(boolean outCancel) {
        return this;
    }

    @Override
    public DialogBuilder setGravity(int gravity) {

        return this;
    }

    @Override
    public DialogBuilder setAnimType(int animType) {
        return this;
    }

    @Override
    public DialogBuilder setAnimRes(int AnimRes) {
        return this;
    }

    @Override
    public DialogBuilder setSaveState(boolean saveState) {
        return this;
    }

    public DialogBuilder setFragmentManager(FragmentManager fragemtManager){
        return this;
    }


    @Override
    public CustomDialog createDialog() 
        return null;
    }

}

```

```

//创建自定义的弹窗

public class CustomDialog implements DialogPower {
	@Override
    public void showDialog() {
       
    }

    @Override
    public void closeDialog() {
        
    }

    @Override
    public void setUIHandler(UIHandler handler) {
      
    }
}
```


芝点Android团队.

