# 最火Android开源项目IjkPlayer使用
---
开源地址：[https://github.com/open-android/IjkPlayer](https://github.com/open-android/IjkPlayer "开源项目地址")


# 运行效果
![](http://i.imgur.com/KO9RoLe.gif)

* 爱生活,爱学习,更爱做代码的搬运工,分类查找更方便请下载黑马助手app


![黑马助手.png](http://upload-images.jianshu.io/upload_images/4037105-f777f1214328dcc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


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


* 获取服务器数据推荐使用github最火开源项目[RetrofitUtils](http://blog.csdn.net/mwq384807683/article/details/53611961).

* 详细的使用方法在DEMO里面都演示啦,如果你觉得这个库还不错,请赏我一颗star吧~~~

* 欢迎关注微信公众号

![](http://oi5nqn6ce.bkt.clouddn.com/itheima/booster/code/qrcode.png)


