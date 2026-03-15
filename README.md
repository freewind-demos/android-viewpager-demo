# Android ViewPager 页面滑动演示

## 简介

本 Demo 演示 ViewPager 的基本用法，展示如何实现横向页面滑动。

## 基本原理

ViewPager 是 Android 提供的页面滑动组件，允许用户通过左右滑动浏览多个页面。通常与 Fragment 和 TabLayout 配合使用，实现标签页滑动效果。

核心组件：
- **ViewPager**：滑动容器
- **PagerAdapter**：页面适配器
- **FragmentPagerAdapter**：适合少量页面（常驻内存）
- **FragmentStatePagerAdapter**：适合大量页面（不常驻）

## 启动和使用

### 环境要求
- Android Studio
- JDK 17
- Gradle 8.x

### 安装和运行

1. 用 Android Studio 打开项目
2. 连接 Android 设备或模拟器
3. 点击 Run 运行

### 使用方法
- 左右滑动屏幕切换页面

## 教程

### 什么是 ViewPager？

ViewPager 是 Android 提供的横向滑动组件，提供了类似 ViewFlipper 的滑动效果，但更流畅、功能更丰富。它常用于：
- 图片画廊
- 引导页
- 标签页内容切换

### 基本用法

1. 在布局中添加 ViewPager：

```xml
<androidx.viewpager.widget.ViewPager
    android:id="@+id/viewPager"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

2. 创建 PagerAdapter：

```kotlin
class MyPagerAdapter(fm: FragmentManager) : FragmentPagerAdapter(fm) {
    override fun getCount(): Int = 3

    override fun getItem(position: Int): Fragment {
        return when (position) {
            0 -> PageFragment()
            1 -> PageFragment()
            else -> PageFragment()
        }
    }
}
```

3. 设置 Adapter：

```kotlin
viewPager.adapter = MyPagerAdapter(supportFragmentManager)
```

### PagerAdapter 类型

1. **PagerAdapter**：基类适配器，适用于 View
2. **FragmentPagerAdapter**：适用于少量固定页面，Fragment 常驻内存
3. **FragmentStatePagerAdapter**：适用于大量页面，不常用的 Fragment 会销毁

## 关键代码详解

### MainActivity.kt

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 1. 获取 ViewPager 组件
        val viewPager = findViewById<ViewPager>(R.id.viewPager)

        // 2. 设置 Adapter
        // 使用 supportFragmentManager 管理 Fragment
        viewPager.adapter = MyPagerAdapter(supportFragmentManager)
    }
}
```

### MyPagerAdapter.kt

```kotlin
class MyPagerAdapter(fm: FragmentManager) : FragmentPagerAdapter(fm) {

    // 返回页面数量
    override fun getCount(): Int = 3

    // 返回指定位置的 Fragment
    override fun getItem(position: Int): Fragment {
        // 返回空白 Fragment
        // 实际项目中可以根据 position 返回不同的 Fragment
        return Fragment()
    }
}
```

### activity_main.xml

```xml
<!-- 根布局：垂直线性布局 -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- 标题 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="ViewPager 页面滑动演示"
        android:gravity="center"
        android:padding="16dp" />

    <!-- ViewPager 组件 -->
    <androidx.viewpager.widget.ViewPager
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```

### ViewPager vs TabLayout 配合

```kotlin
// 连接 ViewPager 和 TabLayout
TabLayoutMediator(tabLayout, viewPager) { tab, position ->
    tab.text = "页面 ${position + 1}"
}.attach()
```
