# ImageSelector

------

图片选择器, 支持多图选择和图片预览等功能。

开源地址：[https://github.com/open-android/ImageSelector](https://github.com/open-android/ImageSelector)

简 书:[http://www.jianshu.com/p/942bf1aa9618](http://www.jianshu.com/p/942bf1aa9618 "选择多张图片")

> 1. 支持`jitpack`
> 2. 支持选择多张
> 3. 支持选择图片数量上限
> 4. 支持图片选择顺序
> 5. 支持图片预览

![](http://upload-images.jianshu.io/upload_images/4037105-dd695310bb187ac2.gif?imageMogr2/auto-orient/strip)


* 爱生活,爱学习,更爱做代码的搬运工,分类查找更方便请下载黑马助手app


![黑马助手.png](http://upload-images.jianshu.io/upload_images/4037105-f777f1214328dcc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 使用步骤

### 1. 在project的build.gradle添加如下代码(如下图)

	allprojects {
	    repositories {
	        maven { url "https://jitpack.io" }
	    }
	}

![](http://upload-images.jianshu.io/upload_images/4037105-2faa5daca3bfe8a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	

### 2. 在Module的build.gradle添加依赖

      compile 'com.github.open-android:ImageSelector:0.1.0'
### 3. 配置如下权限

     <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
     <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
	 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	 <uses-permission android:name="android.permission.CAMERA"/>
     
### 4.复制如下代码到xml布局
 
     <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:onClick="selectImg"
        android:text="@string/image_selector_select_image" />

	    <ScrollView
	        android:layout_width="match_parent"
	        android:layout_height="match_parent">
	
	        <TextView
	            android:id="@+id/content"
	            android:layout_width="match_parent"
	            android:layout_height="wrap_content" />
	    </ScrollView>


### 5.复制如下代码到java类当中
    

  
  
    public class MainActivity extends AppCompatActivity {

	    private static final int REQUEST_CODE_SELECT_IMG = 1;
	    private static final int MAX_SELECT_COUNT = 9;
        private TextView mContentTv;

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        initView();
	    }

	    private void initView() {
	        mContentTv = (TextView) findViewById(R.id.content);
	    }

	    @Override
	    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	        if (requestCode == REQUEST_CODE_SELECT_IMG) {
	            showContent(data);
	            return;
	        }
	
	        super.onActivityResult(requestCode, resultCode, data);
	    }

	    private void showContent(Intent data) {
	        List<String> paths = ImageSelector.getImagePaths(data);
	        if (paths.isEmpty()) {
	            mContentTv.setText(R.string.image_selector_select_none);
	            return;
	        }
	
	        mContentTv.setText(paths.toString());
	    }

	    public void selectImg(View v) {
	        ImageSelector.show(this, REQUEST_CODE_SELECT_IMG, MAX_SELECT_COUNT);
	    }}


* 详细的使用方法在DEMO里面都演示啦,如果你觉得这个库还不错,请赏我一颗star吧~~~

* 欢迎关注微信公众号

![](http://upload-images.jianshu.io/upload_images/4037105-8f737b5104dd0b5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
