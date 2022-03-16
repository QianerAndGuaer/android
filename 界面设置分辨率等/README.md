# 界面设置分辨率等

### AndroidMainfest.xml  安卓配置
``` xml 
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapplication">

    <application
        android:allowBackup="true"  //允许放回
        android:icon="@mipmap/ic_launcher" //设置icon路径
        android:label="@string/app_name" //设置表头
        android:supportsRtl="true"
        android:extractNativeLibs = "true"
        >
        <activity

            android:name=".MainActivity"
            android:screenOrientation="sensorLandscape" //设置横屏且可翻转
            android:exported="true" //适配android版本
            android:theme="@style/Theme.TempThemes" //设置风格
            >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>

```
### themes.xml
``` xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.TempThemes" parent="@android:style/Theme.NoTitleBar.Fullscreen">
        //全屏设置
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowNoTitle">true</item>
        //底图颜色
        <item name="android:windowBackground">@android:color/white</item>
    </style>
</resources>
```
### Activity设置
``` JAVA
 protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //获取手机物理宽高
        WindowManager wm = (WindowManager)  getApplicationContext().getSystemService(Context.WINDOW_SERVICE);
        Display display = wm.getDefaultDisplay();
        DisplayMetrics metrics = new DisplayMetrics();
        display.getRealMetrics(metrics);
         width = metrics.widthPixels;
         height = metrics.heightPixels;

         View decorView = getWindow().getDecorView();
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
                // 全屏显示，隐藏状态栏和导航栏，拉出状态栏和导航栏显示一会儿后消失。
                decorView.setSystemUiVisibility(
                                 View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                                | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                                | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
                                | View.SYSTEM_UI_FLAG_FULLSCREEN
                                | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY
                );
            } else {
                // 全屏显示，隐藏状态栏
                decorView.setSystemUiVisibility(View.SYSTEM_UI_FLAG_FULLSCREEN);
            }
        }
        getWindow().getAttributes().layoutInDisplayCutoutMode = WindowManager.LayoutParams.LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES; //提供的去除刘海方法！ 这里是关键

        setContentView(R.layout.activity_main);
        mFrameLayout = findViewById(R.id.gameView);

    }

```