# 实验四 **Intent**

**本实验通过自定义 WebViewWebView WebView 加载 URL 来验证隐式 Intent Intent 的使用。** 

## 新建一个工程获取URL并启动intent

activity_layout.xml

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal">
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/urlinput"
        android:hint="@string/web_url"
        android:textSize="30sp"
        android:autofillHints="" />
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Go"
        android:textSize="30sp"
        android:background="@color/colorAccent"
        android:layout_gravity="center"
        android:gravity="center" />
    <WebView
        android:layout_width="wrap_content"
        android:id="@+id/web"
        android:layout_height="wrap_content">
    </WebView>

</LinearLayout>
```

strings.xml

```
<resources>
    <string name="app_name">webview</string>
    <string name="browse" />
    <string name="inputUrl" />
    <string name="input" />
    <string name="btn_browse" />
    <string name="hint_edit" />
    <string name="web_url">请输入URL</string>
    <string name="go">Go</string>
</resources>

```

mainactivity.java

```
package com.example.intent;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {
    Button mButton;
    EditText mEditText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        startBrowser();
    }

    boolean startBrowser() {
        mButton = findViewById(R.id.button);
        mEditText = findViewById(R.id.urlinput);
        mButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent();
                intent.setAction(Intent.ACTION_VIEW);
                String url = "https://" + mEditText.getText().toString();
                intent.setData(Uri.parse(url));
                startActivity(intent);
            }
        });
        return true;
    }
}package com.example.webview;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import org.w3c.dom.Text;

public class MainActivity extends AppCompatActivity {
    EditText editText;
    Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        button =(Button) findViewById(R.id.button);
        editText  =(EditText)findViewById(R.id.input);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent();
                String uri="";
                intent.setAction(Intent.ACTION_VIEW);
                uri=button.getText().toString();
                intent.setData(Uri.parse(uri));
                startActivity(intent);
            }
        });

    }


}
```

运行截图：

![27](../image/27.png)



![28](../image/28.png)

## 新建一个工程使用webview加载url

activity.mxl

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal">
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/urlinput"
        android:hint="@string/web_url"
        android:textSize="30sp"
        android:autofillHints="" />
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Go"
        android:textSize="30sp"
        android:background="@color/colorAccent"
        android:layout_gravity="center"
        android:gravity="center" />
    <WebView
        android:layout_width="wrap_content"
        android:id="@+id/web"
        android:layout_height="wrap_content">
    </WebView>

</LinearLayout>
```

strings.xml

```
<resources>
    <string name="app_name">webview</string>
    <string name="browse" />
    <string name="inputUrl" />
    <string name="input" />
    <string name="btn_browse" />
    <string name="hint_edit" />
    <string name="web_url">请输入URL</string>
    <string name="go">Go</string>
</resources>

```

mainactivity.java

```
package com.example.myweb;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;
import android.widget.EditText;

import java.net.URL;

public class MainActivity extends AppCompatActivity {
    EditText editText;
    Button button;
    @Override
    protected  void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        button=findViewById(R.id.button);
        editText  =(EditText)findViewById(R.id.urlinput);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent();
                String uri="";
                uri=editText.getText().toString();
                intent.setData(Uri.parse(uri));
                intent.setAction(Intent.ACTION_VIEW);
                startActivity(intent);
            }
        });

        Intent intent=getIntent();
        Uri data = intent.getData();
        URL url=null;
        try{
            url=new URL(data.getScheme(),data.getHost(),data.getPath());
            startBroswer(url);
        }
        catch (Exception e){
            e.printStackTrace();
        }

    }
    private void startBroswer(URL url){
        WebView web=findViewById(R.id.web);
        web.loadUrl(url.toString());
        web.setWebViewClient(new WebViewClient(){
            @Override
            public boolean shouldOverrideUrlLoading(WebView v,String url){
                v.loadUrl(url);
                return true;
            }
        });
    }
}
```

![29](../image/29.png)



![30](../image/30.png)