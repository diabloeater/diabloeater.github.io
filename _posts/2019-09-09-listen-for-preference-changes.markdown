---
layout: post
title: 在PreferenceFragment監聽設定變更
date:   2019-09-09 20:13:08 +0800
categories: android
author: "鬼面散人"
---

起初是因為需要在app加入一些簡單的設定功能而開始使用[Preference API][preference-doc]，其實原本在用的是`PreferenceActivity`，但是這樣一來主畫面上方的ActionBar就消失了（愈看愈奇怪XD）。所以想說趁著這次改版順便換成`PreferenceFragment`。沒想到改完之後發現，變更設定後原本會立即執行的功能不work了，於是立刻下了中斷點查看，結果發現變更設定完成後並沒有執行`onSharedPreferenceChanged`方法。


## 解決辦法：

覆寫`PreferenceFragment`類別的`onResume()`和`onPause()`方法。在其中分別加入`registerOnSharedPreferenceChangeListener`和`unregisterOnSharedPreferenceChangeListener`以重新註冊及註銷監聽，就可以了。


## 示例：


{% highlight java %}
public class CustomPreferenceFragment extends PreferenceFragment implements SharedPreferences.OnSharedPreferenceChangeListener {


    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.preferences);
    }

    @Override
    public void onResume() {
        super.onResume();
        // 註冊偏好變更監聽器
        getPreferenceManager().getSharedPreferences().registerOnSharedPreferenceChangeListener(this);

    }

    @Override
    public void onPause() {
        // 註銷偏好變更監聽器
        getPreferenceManager().getSharedPreferences().unregisterOnSharedPreferenceChangeListener(this);
        super.onPause();
    }

    @Override
    public void onSharedPreferenceChanged(SharedPreferences sharedPreferences, String key) {
        // TODO: 當偏好發生變更時要執行的動作
    }
}
{% endhighlight %}


[preference-doc]: https://developer.android.com/reference/android/preference/Preference.html?hl=zh-tw
