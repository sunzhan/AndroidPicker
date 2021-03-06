# Summary
[![API Level](https://img.shields.io/badge/API-9%2B-green.svg)](https://github.com/gzu-liyujiang/AndroidPicker)
[![Download](https://api.bintray.com/packages/gzu-liyujiang/maven/WheelPicker/images/download.svg)](http://jcenter.bintray.com/cn/qqtheme/framework/)
[![Download](https://jitpack.io/v/gzu-liyujiang/AndroidPicker.svg)](https://jitpack.io/#gzu-liyujiang/AndroidPicker)
[![Build Status](https://travis-ci.org/gzu-liyujiang/AndroidPicker.svg?branch=master)](https://travis-ci.org/gzu-liyujiang/AndroidPicker)
安卓选择器类库，包括日期选择器、时间选择器、单项选择器、城市选择器、颜色选择器、文件选择器、目录选择器、数字选择器、星座选择器、生肖选择器等，可自定义顶部及底部界面，可自定义窗口动画。
欢迎大伙儿在[Issues](https://github.com/gzu-liyujiang/AndroidPicker/issues)提交你的意见或建议。    
欢迎Fork & Pull requests贡献您的代码。[查看更新日志](https://github.com/gzu-liyujiang/AndroidPicker/blob/master/ChangeLog.md)。     

# Install
“app”是测试用例；“library”包括WheelPicker、ColorPicker、FilePicker，
WheelPicker包括DateTimePicker、OptionPicker、LinkagePicker、AddressPicker、NumberPicker等，
#### 懒人建议直接远程加载jcenter里的
其中latest.release为最新版，也可以[参照此处指定具体的版本号](https://github.com/gzu-liyujiang/AndroidPicker/releases)：
```groovy
dependencies {
    compile 'cn.qqtheme.framework:WheelPicker:latest.release'
    compile 'cn.qqtheme.framework:FilePicker:latest.release'
    compile 'cn.qqtheme.framework:ColorPicker:latest.release'
}
```
#### 需要学习或修改源代码，则下载本项目手动集成
下载示例项目后导入“library”下的相关module到你的项目（记得将module下的build.gradle修改类似于下面的内容，否则可能会报错找不到BuildToolsVersion）：
```groovy
apply plugin: 'com.android.library'

android {
    compileSdkVersion 22
    buildToolsVersion 22.0.1

    defaultConfig {
        minSdkVersion 14
        targetSdkVersion 22
    }
}

dependencies {
    compile project(':Common') //Common模块不需要加此句
}
```
然后依赖（WheelPicker、FilePicker及ColorPicker是独立的，需要用哪个就compile哪个）：
```groovy
dependencies {
    compile project(':WheelPicker')
    compile project(':FilePicker')
    compile project(':ColorPicker')
}
```
# ProGuard
由于地址选择器使用了[fastjson](https://github.com/alibaba/fastjson)来解析，混淆时候需要加入以下类似的规则，不混淆Province、City等实体类。
```
-keepattributes InnerClasses,Signature
-keepattributes *Annotation*

-keep class cn.qqtheme.framework.entity.** { *;}
-keep class cn.qqtheme.framework.picker.AddressPicker$* { *;}
```

# Method
void setFillScreen(boolean fillScreen)
固定高度为屏幕的高     
void setGravity(int gravity)
位于屏幕何处     
void setHalfScreen(boolean halfScreen)
固定高度为屏幕的一半     
void setHeight(int height)
设置弹窗的高     
void setSize(int width, int height)
设置弹窗的宽和高     
void setWidth(int width)
设置弹窗的宽     
void setLineColor(int lineColor)
设置分隔线颜色     
void setLineVisible(boolean lineVisible)
设置分隔线是否可见     
void setOffset(int offset)
设置选项偏移量，默认为1，范围为1~4。     
void setTextColor(int textColor)
设置文字颜色     
void setTextColor(int textColorFocus, int textColorNormal)
设置文字颜色     
void setTextSize(int textSize)
设置文字大小     
void setCancelText(java.lang.CharSequence cancelText)
设置顶部标题栏取消按钮文字     
void setCancelText(int textRes)
设置顶部标题栏取消按钮文字     
void setCancelTextColor(int cancelTextColor)
设置顶部标题栏取消按钮文字颜色     
void setCancelTextSize(int cancelTextSize)
设置顶部标题栏取消按钮文字大小（单位为sp）     
void setCancelVisible(boolean cancelVisible)
设置顶部标题栏取消按钮是否显示     
void setSubmitText(java.lang.CharSequence submitText)
设置顶部标题栏确定按钮文字     
void setSubmitText(int textRes)
设置顶部标题栏确定按钮文字     
void setSubmitTextColor(int submitTextColor)
设置顶部标题栏确定按钮文字颜色     
void setSubmitTextSize(int submitTextSize)
设置顶部标题栏确定按钮文字大小（单位为sp）     
void setTitleText(java.lang.CharSequence titleText)
设置顶部标题栏标题文字     
void setTitleText(int textRes)
设置顶部标题栏标题文字     
void setTitleTextColor(int titleTextColor)
设置顶部标题栏标题文字颜色     
void setTitleTextSize(int titleTextSize)
设置顶部标题栏标题文字大小（单位为sp）     
void setTopBackgroundColor(int topBackgroundColor)
设置顶部标题栏背景颜色     
void setTopHeight(int topHeight)
设置顶部标题栏高度（单位为dp）     
void setTopLineColor(int topLineColor)
设置顶部标题栏下划线颜色     
void setTopLineVisible(boolean topLineVisible)
设置顶部标题栏下划线是否显示    
......   

# Custom
#### 自定义窗口进入退出动画(可选)
推荐使用[ViewAnimator](https://github.com/gzu-liyujiang/ViewAnimator)这个动画库来实现：
```groovy
dependencies {
    compile 'com.github.florent37:viewanimator:1.0.3'
}
```
```java
        ViewAnimator.animate(picker.getRootView())
                .slideBottomIn()
                .interpolator(new AccelerateInterpolator())
                .start();
```
或者使用XML定义动画：
```xml
<resources>
    <style name="Animation.CustomPopup" parent="@android:style/Animation">
        <item name="android:windowEnterAnimation">@anim/popup_in</item>
        <item name="android:windowExitAnimation">@anim/popup_out</item>
    </style>
</resources>
```
```java
    picker.setAnimationStyle(R.style.Animation_CustomPopup);
```

#### 自定义顶部及底部界面
添加自己的类，继承自现有的选择器，覆盖makeHeaderView、makeFooterView、onSubmit、onCancel，在确定选择时调用onSubmit，
取消选择时调用onCancel。详见示例：[CustomHeaderAndFooterPicker.java](https://github.com/gzu-liyujiang/AndroidPicker/blob/master/app/src/main/java/cn/qqtheme/androidpicker/CustomHeaderAndFooterPicker.java)。

# Sample （更多用法详见示例项目）
自定义选择器：
```java
        CustomHeaderAndFooterPicker picker = new CustomHeaderAndFooterPicker(this);
        picker.setGravity(Gravity.CENTER);//居中
        picker.setOnOptionPickListener(new OptionPicker.OnOptionPickListener() {
            @Override
            public void onOptionPicked(int position, String option) {
                showToast(option);
            }
        });
        picker.show();
```

日期选择器：
```java
        DatePicker picker = new DatePicker(this, DatePicker.YEAR_MONTH_DAY);
        picker.setRangeStart(2016, 8, 29);//开始范围
        picker.setRangeEnd(2022, 1, 1);//结束范围
        picker.setOnDatePickListener(new DatePicker.OnYearMonthDayPickListener() {
            @Override
            public void onDatePicked(String year, String month, String day) {
                showToast(year + "-" + month + "-" + day);
            }
        });
        picker.show();
```

时间选择器：
```java
        TimePicker picker = new TimePicker(this, TimePicker.HOUR_12);
        picker.setRangeStart(9, 0);//09:00
        picker.setRangeEnd(12, 30);//12:30
        picker.setTopLineVisible(false);
        picker.setOnTimePickListener(new TimePicker.OnTimePickListener() {
            @Override
            public void onTimePicked(String hour, String minute) {
                showToast(hour + ":" + minute);
            }
        });
        picker.show();
```

单项选择器（可用于性别、学历、职业、星座等选择）：
```java
        OptionPicker picker = new OptionPicker(this, new String[]{
                "第一项", "第二项", "这是一个很长很长很长很长很长很长很长很长很长的很长很长的很长很长的项"
        });
        picker.setOffset(2);
        picker.setSelectedIndex(1);
        picker.setTextSize(11);
        picker.setOnOptionPickListener(new OptionPicker.OnOptionPickListener() {
            @Override
            public void onOptionPicked(String option) {
                showToast(option);
            }
        });
        picker.show();
```

数字选择器(可用于身高、体重、年龄等选择)：
```java
        NumberPicker picker = new NumberPicker(this);
        picker.setOffset(2);//偏移量
        picker.setRange(145, 200, 1);//数字范围
        picker.setSelectedItem(172);
        picker.setLabel("厘米");
        picker.setOnOptionPickListener(new OptionPicker.OnOptionPickListener() {
            @Override
            public void onOptionPicked(String option) {
                showToast(option);
            }
        });
        picker.show();
```

二三级联动选择器（详见示例项目，参见地址选择器）

地址选择器（含省级、地级、县级）：
```java
        ArrayList<Province> data = new ArrayList<Province>();
        String json = AssetsUtils.readText(this, "city.json");
        data.addAll(JSON.parseArray(json, Province.class));
        AddressPicker picker = new AddressPicker(this, result);
        picker.setSelectedItem("贵州", "贵阳", "花溪");
        //picker.setHideProvince(true);//加上此句举将只显示地级及县级
        //picker.setHideCounty(true);//加上此句举将只显示省级及地级
        //picker.setColumnWeight(2/8.0, 3/8.0, 3/8.0);//省级、地级和县级的比例为2:3:3
        picker.setOnAddressPickListener(new AddressPicker.OnAddressPickListener() {
            @Override
            public void onAddressPicked(Province province, City city, County county) {
                showToast(province + city + county);
            }
        });
        picker.show();
```

星座选择器：
```java
        OptionPicker picker = new OptionPicker(this, new String[]{
                "水瓶", "双鱼", "白羊", "金牛", "双子", "巨蟹", "狮子", "处女", "天秤", "天蝎", "射手", "摩羯",
        });
        picker.setLabel("座");
        picker.setTopBackgroundColor(0xFFEEEEEE);
        picker.setLineVisible(true);
        picker.setTopLineColor(0xFFEE0000);
        picker.setTopHeight(50);
        picker.setTitleText("请选择");
        picker.setTitleTextColor(0xFF999999);
        picker.setTitleTextSize(24);
        picker.setCancelTextColor(0xFF33B5E5);
        picker.setCancelTextSize(22);
        picker.setSubmitTextColor(0xFF33B5E5);
        picker.setSubmitTextSize(22);
        picker.setTextColor(0xFFFF0000, 0xFF999999);
        picker.setLineColor(0xFFEE0000);
        picker.setSelectedItem("射手");
        picker.setOnOptionPickListener(new OptionPicker.OnOptionPickListener() {
            @Override
            public void onOptionPicked(int position, String option) {
                showToast(option);
            }
        });
        picker.show();
```

颜色选择器：
```java
        ColorPicker picker = new ColorPicker(this);
        picker.setInitColor(0xFFDD00DD);
        picker.setOnColorPickListener(new ColorPicker.OnColorPickListener() {
            @Override
            public void onColorPicked(int pickedColor) {
                showToast(ConvertUtils.toColorString(pickedColor));
            }
        });
        picker.show();
```

文件选择器（需要权限android.permission.READ_EXTERNAL_STORAGE）：
```java
        FilePicker picker = new FilePicker(this, FilePicker.FILE);
        picker.setShowHideDir(false);
        picker.setRootPath(StorageUtils.getRootPath(this) + "Download/");
        //picker.setAllowExtensions(new String[]{".apk"});
        picker.setOnFilePickListener(new FilePicker.OnFilePickListener() {
            @Override
            public void onFilePicked(String currentPath) {
                showToast(currentPath);
            }
        });
        picker.show();
```

目录选择器（需要权限android.permission.READ_EXTERNAL_STORAGE）：
```java
        FilePicker picker = new FilePicker(this, FilePicker.DIRECTORY);
        picker.setOnFilePickListener(new FilePicker.OnFilePickListener() {
            @Override
            public void onFilePicked(String currentPath) {
                showToast(currentPath);
            }
        });
        picker.show();
```

# Thanks
库项目修改使用了以下项目：      
https://github.com/wangjiegulu/WheelView      
https://github.com/jbruchanov/AndroidColorPicker      

# Screenshots
![自定义选择器效果图](/screenshots/custom.gif)   
![日期选择器效果图](/screenshots/date.gif)            
![日期选择器效果图](/screenshots/monthday.jpg)   
![时间选择器效果图](/screenshots/time.gif)   
![单项选择器效果图](/screenshots/option.gif)           
![地址选择器效果图](/screenshots/address.gif)   
![地址选择器效果图](/screenshots/address.png)         
![数字选择器效果图](/screenshots/number.gif)   
![星座选择器效果图](/screenshots/constellation.jpg)   
![颜色选择器效果图](/screenshots/color.gif)    
![文件选择器效果图](/screenshots/file.gif)    
![目录选择器效果图](/screenshots/dir.gif)    

# Contact
<a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=1032694760&site=穿青人&menu=yes"><img border="0" src="http://wpa.qq.com/pa?p=2:1032694760:51" alt="点击这里给我发消息" title="点击这里给我发消息"/></a>
<a target="_blank" href="http://mail.qq.com/cgi-bin/qm_share?t=qm_mailme&email=q8fC0t7BwsrFzIXfwOva2oXIxMY" style="text-decoration:none;"><img src="http://rescdn.qqmail.com/zh_CN/htmledition/images/function/qm_open/ico_mailme_02.png"/></a>

