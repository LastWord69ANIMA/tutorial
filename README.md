# tutorial2 that How I work at android studio

サンプルコードは参考サイトの通りですが、
```
ERROR: AAPT: error: resource style/Theme.Material3.DayNight.NoActionBar (aka com.example.tutorial:style/Theme.Material3.DayNight.NoActionBar) not found.
error: resource style/Theme.Material3.DayNight.NoActionBar (aka com.example.tutorial:style/Theme.Material3.DayNight.NoActionBar) not found.
error: failed linking references.
```

```
Error running 'app': The activity must be exported or contain an intent-filter
```

という2つのエラーが出て、エミュレータが起動できなかったので、補助サイトより対処。

## 一つ目のエラー対処
app/res/theme/themes.xmlにて
```
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Base.Theme.Tutorial" parent="@style/Theme.AppCompat.DayNight.NoActionBar"/>
        <!-- Customize your light theme here. -->
        <!-- <item name="colorPrimary">@color/my_light_primary</item> -->

</resources>
```
nightの方には

```
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Base.Theme.Tutorial" parent="@style/Theme.AppCompat.Light.NoActionBar"/>
        <!-- Customize your light theme here. -->
        <!-- <item name="colorPrimary">@color/my_light_primary</item> -->

</resources>
```
parentにある奴が参照できないため、エラーが出ていましたが、@style/Theme･･･とすると候補に挙がるので、それを選択すると解消。


## 二つ目のエラー対処
app/manifests/AndroidManifest.xmlにて
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AppCompat.Light.NoActionBar"
        tools:targetApi="31">



        <activity
            android:name=".MainActivity" android:exported="true"

            android:theme="@style/Theme.AppCompat.Light.NoActionBar"
        />

    </application>

</manifest>
```
変更点として、
+ android:themeにて、themeを変更
+ activityタグを追加



## 参考サイト

https://appdev-room.com/android-app-develop

## 補助サイト
（manifestのactivity,NoActionBar及びエミュレート関連）

https://qiita.com/crthgt6t/items/f0112c9c3615214927b1

https://stackoverflow.com/questions/68610721/android-studio-the-activity-must-be-exported-or-contain-an-intent-filter

https://zenn.dev/imokeeeenpi/articles/38d8b72e4dd442

https://pg.akihiro-takeda.com/android-avd-chgini/
