# JSON과 XML
api를 파싱하는 데이터 형식에는 JSON형식과 XML형식이 있다고 들었다. 

XML과 JSON은 데이터를 전송하기위한 데이터 포맷 형식이라고만 알고 있고 차이를 정확히 모르기 때문에 정리를 해보았다.

## JSON
JSON은 JavaScript Object Notation의 약자로, 데이터를 저장하거나 전송할 때 많이 사용되는 데이터 교환 형식이다. 최근에는 용량이 작아서 JSON이 XML을 대체에서 데이터 전송 등에 많이 사용한다. 


### JSON의 특징

## XML이란?
XML은 EXtensible Markup Language의 약자로, HTML과 매우 비슷한 문자 기반으 마크업 언어이다.

XML은 HTML처럼 데이터를 보여주는 목적이 아닌, 데이터를 저장하고 전달할 목적으로만 만들어졌다.
또한, XML 태그는 HTML 태그처럼 미리 정의되어 있지 않고, 사용자가 직접 정의할 수 있다.

## JSON parse

activity_main.xml
``` xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".MainActivity">

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="json parse"
        android:onClick="clickBtn"/>
    <TextView
        android:id="@+id/tv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:padding="8dp"/>

</LinearLayout>
```
MainActivity.java
``` java
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.content.res.AssetManager;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

public class MainActivity extends AppCompatActivity {

    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tv = findViewById(R.id.tv);
    }
    public void clickBtn(View view) {

        //json 파일 읽어와서 분석하기

        //assets폴더의 파일을 가져오기 위해
        //창고관리자(AssetManager) 얻어오기
        AssetManager assetManager = getAssets();

        //assets/ test.json 파일 읽기 위한 InputStream
        try {
            InputStream is = assetManager.open("jsons/test.json");
            InputStreamReader isr = new InputStreamReader(is);
            BufferedReader reader = new BufferedReader(isr);

            StringBuffer buffer = new StringBuffer();
            String line = reader.readLine();
            while (line != null) {
                buffer.append(line + "\n");
                line = reader.readLine();
            }

            String jsonData = buffer.toString();

            //json 데이터가 하나의 배열일 때
            //json 객체 생성
//            JSONObject jsonObject= new JSONObject(jsonData);
//            String name= jsonObject.getString("name");
//            String msg= jsonObject.getString("msg");
//
//            tv.setText("이름 : "+name+"\n"+"메세지 : "+msg);

            //json 데이터가 []로 시작하는 여러 배열일때..
            //JSONArray 객체 생성
            JSONArray jsonArray = new JSONArray(jsonData);

            String s = "";

            for (int i = 0; i < jsonArray.length(); i++) {
                JSONObject jo = jsonArray.getJSONObject(i);

                String name = jo.getString("name");
                String msg = jo.getString("msg");
                JSONObject flag = jo.getJSONObject("birthday");
                int aa = flag.getInt("month");
                int bb = flag.getInt("day");

                s += name + " : " + msg + ", 생일 :  " + aa + "월" + bb + "일\n";
            }
            tv.setText(s);

        } catch (IOException e) {
            e.printStackTrace();
        } catch (JSONException e) {
            e.printStackTrace();
        }

    }
}
```
test.json
``` json
[
  {"name":  "제갈은", "msg":  "경기도 안산", "birthday": {"month":  3, "day":  23}},
  {"name":  "심세영","msg":  "경기도 안양", "birthday": {"month": 6,"day": 19}}
]
```
### 결과 화면
<img width="431" alt="jsonparse" src="https://user-images.githubusercontent.com/43868540/86513605-89604f80-be46-11ea-91d9-30d9d99a6acf.png">

## XML parse
activity_main.xml
``` xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".MainActivity">

    <TableLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:stretchColumns="1">

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:textSize="24sp"
                android:text="No" />

            <EditText
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginLeft="20dp"
                android:textSize="24sp"
                android:id="@+id/editTextNo"/>
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:textSize="24sp"
                android:text="Name" />

            <EditText
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginLeft="20dp"
                android:textSize="24sp"
                android:id="@+id/editTextName"/>
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:textSize="24sp"
                android:text="Phone" />

            <EditText
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginLeft="20dp"
                android:textSize="24sp"
                android:id="@+id/editTextPhone"/>
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:textSize="24sp"
                android:text="Over20" />

            <CheckBox
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginLeft="20dp"
                android:textSize="24sp"
                android:id="@+id/checkBoxOver20"
                android:text="Over 20 years?"/>
        </TableRow>

    </TableLayout>

</LinearLayout>
```
MainActivity.java
``` java
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.content.res.AssetManager;
import android.os.Bundle;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;
import org.xmlpull.v1.XmlPullParser;
import org.xmlpull.v1.XmlPullParserFactory;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

public class MainActivity extends AppCompatActivity {

    TextView tv;
    final int STEP_NONE = 0 ;
    final int STEP_NO = 1 ;
    final int STEP_NAME = 2 ;
    final int STEP_PHONE = 3 ;
    final int STEP_OVER20 = 4 ;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        AssetManager am = getResources().getAssets();
        InputStream is = null;

        try {
            int no = -1;
            String name = null;
            String phone = null;
            boolean isOver20 = false;

            // XML 파일 스트림 열기
            is = am.open("test2.xml");

            // XML 파서 초기화
            XmlPullParserFactory parserFactory = XmlPullParserFactory.newInstance();
            XmlPullParser parser = parserFactory.newPullParser();

            // XML 파서에 파일 스트림 지정.
            parser.setInput(is, "UTF-8");

            int eventType = parser.getEventType();
            int step = STEP_NONE ;
            while (eventType != XmlPullParser.END_DOCUMENT) {
                if (eventType == XmlPullParser.START_DOCUMENT) {
                    // XML 데이터 시작
                } else if (eventType == XmlPullParser.START_TAG) {
                    String startTag = parser.getName();
                    if (startTag.equals("NO")) {
                        step = STEP_NO;
                    } else if (startTag.equals("NAME")) {
                        step = STEP_NAME;
                    } else if (startTag.equals("PHONE")) {
                        step = STEP_PHONE;
                    } else if (startTag.equals("OVER20")) {
                        step = STEP_OVER20;
                    } else {
                        step = STEP_NONE;
                    }
                } else if (eventType == XmlPullParser.END_TAG) {
                    String endTag = parser.getName();
                    if ((endTag.equals("NO") && step != STEP_NO) ||
                            (endTag.equals("NAME") && step != STEP_NAME) ||
                            (endTag.equals("PHONE") && step != STEP_PHONE) ||
                            (endTag.equals("OVER20") && step != STEP_OVER20)) {
                        // TODO : error
                    }
                    step = STEP_NONE;
                } else if (eventType == XmlPullParser.TEXT) {
                    String text = parser.getText();
                    if (step == STEP_NO) {
                        try {
                            no = Integer.parseInt(text);
                        } catch (Exception e) {
                            no = 0;
                        }
                    } else if (step == STEP_NAME) {
                        name = text;
                    } else if (step == STEP_PHONE) {
                        phone = text;
                    } else if (step == STEP_OVER20) {
                        isOver20 = Boolean.parseBoolean(text);
                    }
                }

                eventType = parser.next();
            }

            if (no == -1 || name == null || phone == null) {
                // ERROR : XML is invalid.
            } else {

                EditText editTextNo = (EditText) findViewById(R.id.editTextNo);
                editTextNo.setText(Integer.toString(no));

                EditText editTextName = (EditText) findViewById(R.id.editTextName);
                editTextName.setText(name);

                EditText editTextPhone = (EditText) findViewById(R.id.editTextPhone);
                editTextPhone.setText(phone);

                CheckBox checkBoxOver20 = (CheckBox) findViewById(R.id.checkBoxOver20);
                checkBoxOver20.setChecked(isOver20);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

}
```

test2.xml
``` xml
<?xml version="1.0" encoding="utf-8"?>
<CONTACT>
    <NO>1</NO>
    <NAME>제갈은</NAME>
    <PHONE>010-2614-6938</PHONE>
    <OVER20>true</OVER20>
</CONTACT>
```

### 결과화면
<img width="419" alt="xmlparse" src="https://user-images.githubusercontent.com/43868540/86514641-4efab080-be4e-11ea-9efb-311c2c7ed013.png">

