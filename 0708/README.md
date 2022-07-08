# Android DB연동

### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ListView
            android:id="@+id/lstMember"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
    </RelativeLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```

### MainActivity.java
```java
package com.inhatc.android_dbsqlite1;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    SQLiteDatabase myDB;
    SimpleAdapter myADT;
    ArrayList<String> aryMBRList;
    ArrayAdapter<String> adtMembers;
    ListView lstView;
    String strRecord = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        myDB = this.openOrCreateDatabase("PhoneBook", MODE_PRIVATE, null);
        myDB.execSQL("Drop table if exists members");

        myDB.execSQL("Create table members (" + "_id integer primary key autoincrement, " +
                "Name text not null, " + "Phone_No text not null);" );
        myDB.execSQL("Insert into members " + " (Name, Phone_No) values ('kdhong', '011-1234-5678');") ;

        ContentValues insertValue = new ContentValues();
        insertValue.put("Name", "Juliet");
        insertValue.put("Phone_No", "010-123-4567");
        myDB.insert("members", null, insertValue);

        ContentValues insertValue1 = new ContentValues();
        insertValue1.put("Name", "Yunoi");
        insertValue1.put("Phone_No", "010-3328-7004");
        myDB.insert("members", null, insertValue1);

        Cursor allRCD = myDB.query("members", null, null, null, null, null, null, null);

        aryMBRList = new ArrayList<String>();
        if (allRCD != null) {
            if (allRCD.moveToFirst()) {
                do {
                    strRecord = allRCD.getString(1) + "\t\t" + allRCD.getString(2);
                    aryMBRList.add(strRecord);

                }while(allRCD.moveToNext());
            }
        }

        adtMembers = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_single_choice, aryMBRList);

        lstView = (ListView) findViewById(R.id.lstMember);
        lstView.setAdapter(adtMembers);
        lstView.setChoiceMode(ListView.CHOICE_MODE_SINGLE);

        if (myDB != null) myDB.close();

    }
}
```
