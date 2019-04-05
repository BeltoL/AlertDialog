# 创建自定义布局的AlertDialog
## 创建如图所示的自定义对话框  请创建一个如图所示的布局，调用 AlertDialog.Builder 对象上的 setView() 将布局添加到 AlertDialog。
![仿真机截图](https://img-blog.csdnimg.cn/20190405230538475.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/clickme"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:text="点我"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</android.support.constraint.ConstraintLayout>
```

alertdialog.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="AlertAialog"
            android:textSize="50dp"
            android:textColor="#fff"
            android:gravity="center"
            android:background="#FFD700"
            android:paddingTop="20dp"
            android:paddingBottom="20dp"/>
    </LinearLayout>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:layout_marginTop="10dp">
        <EditText

            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Username"
            android:layout_marginLeft="5dp"
            android:layout_marginRight="5dp"/>
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Password"
            android:inputType="textPassword"
            android:layout_marginLeft="5dp"
            android:layout_marginRight="5dp"/>
    </LinearLayout>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginTop="10dp">

        <Button
            android:id="@+id/cancle"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center"
            android:text="Cancel"
            android:textColor="#000" />
        <Button
            android:id="@+id/signin"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Sign in"
            android:textColor="#000"
            android:gravity="center"
            android:layout_weight="1"/>
    </LinearLayout>

</LinearLayout>
```

MainActivity.java
```
package com.example.cy5962.alertdialog_demo;

import android.content.Context;
import android.support.v7.app.AlertDialog;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button bn=(Button)findViewById(R.id.clickme);
        LayoutInflater inflater=MainActivity.this.getLayoutInflater();
        View v=inflater.inflate(R.layout.alertdialog,null,false);
        Context context=MainActivity.this;
        AlertDialog.Builder builder=new AlertDialog.Builder(context);

        builder.setView(v);

        builder.setCancelable((false));

        final AlertDialog alertDialog=builder.create();
        bn.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v){
                alertDialog.show();
            }
        });

        v.findViewById(R.id.cancle).setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View view){
                Toast.makeText(MainActivity.this, "cancle", Toast.LENGTH_LONG).show();
                alertDialog.dismiss();
            }
        });

        v.findViewById(R.id.signin).setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View view){
                Toast.makeText(MainActivity.this,"Sign in",Toast.LENGTH_LONG).show();
                alertDialog.dismiss();
            }
        });
    }
}
```