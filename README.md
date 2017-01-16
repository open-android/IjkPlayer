# 最火Android开源项目IjkPlayer使用
---
开源地址：[https://github.com/open-android/IjkPlayer](https://github.com/open-android/IjkPlayer "开源项目地址")


# 运行效果
![](http://i.imgur.com/KO9RoLe.gif)


## 使用步骤

### 1. 在project的build.gradle添加如下代码(如下图)

	allprojects {
	    repositories {
	        ...
	        maven { url "https://jitpack.io" }
	    }
	}

![](http://i.imgur.com/oCPpMNe.png)
	

	
### 2. 在Module的build.gradle添加依赖

     compile 'com.github.open-android:IjkPlayer:1.0.0'

### 3. 复制如下代码到xml

	<com.dl7.player.media.IjkPlayerView
        android:id="@+id/player_view"
        android:layout_width="match_parent"
        android:layout_height="200dp"/>


### 4. 复制如下代码到Activity

		mPlayerView = (IjkPlayerView) findViewById(R.id.player_view);
        mUri = Uri.parse("http://covertness.qiniudn" +
                ".com/android_zaixianyingyinbofangqi_test_baseline.mp4");

        mPlayerView.init()
                      .setVideoPath(mUri) 
                .setMediaQuality(IjkPlayerView.MEDIA_QUALITY_HIGH)
                .enableDanmaku()
                .start();


### 5.把player的生命周期和Activty生命周期进行绑定


	 @Override
    protected void onResume() {
        super.onResume();
        mPlayerView.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
        mPlayerView.onPause();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        mPlayerView.onDestroy();
    }

    @Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        mPlayerView.configurationChanged(newConfig);
    }

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if (mPlayerView.handleVolumeKey(keyCode)) {
            return true;
        }
        return super.onKeyDown(keyCode, event);
    }

    @Override
    public void onBackPressed() {
        if (mPlayerView.onBackPressed()) {
            return;
        }
        super.onBackPressed();
    }


### 6.添加权限

	<uses-permission android:name="android.permission.INTERNET"></uses-permission>


> 细节注意:
>
> mPlayerView:表示视频播放的view
>
>mUri：表示视频的路径


获取服务器数据推荐使用github最火开源项目[RetrofitUtils](http://blog.csdn.net/mwq384807683/article/details/53611961).

欢迎关注微信公众号

![](http://oi5nqn6ce.bkt.clouddn.com/itheima/booster/code/qrcode.png)


