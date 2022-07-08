# Android Studio, SQLite DB연동

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

        <TextView
            android:id="@+id/txtTitle"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Car Management System"
            android:layout_alignParentLeft="true"
            android:layout_marginTop="17dp"
            android:gravity="center"
            android:textSize="20dp"/>


        <TextView
            android:id="@+id/txtCarType"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="34dp"
            android:layout_alignParentLeft="true"
            android:layout_below="@+id/txtTitle"
            android:layout_marginLeft="5dp"
            android:text="Type : " />

        <EditText
            android:id="@+id/editCarType"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignBaseline="@+id/txtCarType"
            android:layout_alignBottom="@+id/txtCarType"
            android:layout_marginLeft="14dp"
            android:layout_toRightOf="@+id/txtCarType"
            android:ems="8" />

        <TextView
            android:id="@+id/txtCarPower"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/txtCarType"
            android:layout_marginTop="20dp"
            android:layout_marginLeft="5dp"
            android:text="Power : " />

        <EditText
            android:id="@+id/editCarPower"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/editCarType"
            android:layout_alignLeft="@+id/editCarType"
            android:ems="8" />

        <Button
            android:id="@+id/btnInsert"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Insert"
            android:textSize="12dp"
            android:layout_alignParentEnd="true"
            android:layout_alignBottom="@+id/txtCarType"/>

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Update"
            android:textSize="12dp"
            android:layout_alignParentEnd="true"
            android:layout_below="@+id/btnInsert"/>

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Delete"
            android:textSize="12dp"
            android:layout_alignParentEnd="true"
            android:layout_below="@+id/btnUpdate"/>

        <Button
            android:id="@+id/btnSearch"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Search"
            android:textSize="12dp"
            android:layout_alignParentEnd="true"
            android:layout_below="@+id/btnDelete"/>
        <ListView
            android:id="@+id/lstMember"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/btnSearch">

        </ListView>
    </RelativeLayout>
</androidx.constraintlayout.widget.ConstraintLayout>
```


### MainActivity.java
```java
package com.inhatc.android_dbsqlite3;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.SimpleAdapter;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    SQLiteDatabase myDB;
    SimpleAdapter myADT;
    ArrayList<String> aryMBRList;
    ArrayAdapter<String> adtMembers;
    ListView lstView;
    String strRecord = null;
    ContentValues insertValue;
    Cursor allRCD;
    Button btnInsert, btnUpdate, btnDelete, btnSearch;
    EditText edtCarType, edtCarPower;
    String strSQL = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        edtCarType = (EditText) findViewById(R.id.editCarType);
        edtCarPower = (EditText) findViewById(R.id.editCarPower);

        btnInsert = (Button) findViewById(R.id.btnInsert);
        btnUpdate = (Button) findViewById(R.id.btnUpdate);
        btnDelete = (Button) findViewById(R.id.btnDelete);
        btnSearch = (Button) findViewById(R.id.btnSearch);

        btnInsert.setOnClickListener(this);
        btnUpdate.setOnClickListener(this);
        btnDelete.setOnClickListener(this);
        btnSearch.setOnClickListener(this);

        lstView = (ListView) findViewById(R.id.lstMember);
        lstView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id){
                String[] strData = null;
                strData = aryMBRList.get(position).toString().split("\t\t");

                edtCarType.setText(strData[0]);
                edtCarPower.setText(strData[1]);

            }
        });


        myDB = this.openOrCreateDatabase("CarInformation", MODE_PRIVATE, null);
        myDB.execSQL("Drop table if exists Carlist");

        myDB.execSQL("Create table Carlist (" + " _id integer primary key autoincrement, " + "CarType text not null, " + "CarPower text not null);");

        myDB.execSQL("Insert into Carlist " + "(CarType, CarPower) values ('BMW 528i', '2800');" );

        insertValue = new ContentValues();
        insertValue.put("CarType", "Benz 320");
        insertValue.put("CarPower", "3200");
        myDB.insert("Carlist", null, insertValue);

        getDBData(null);

        if(myDB != null) myDB.close();

    }

    public void getDBData(String strWhere) {

        allRCD = myDB.query("Carlist", null, strWhere, null, null, null, null, null);

        aryMBRList = new ArrayList<String>();
        if (aryMBRList != null){
            if (allRCD.moveToFirst()) {
                do{
                    strRecord = allRCD.getString(1) + "\t\t" + allRCD.getString(2);
                    aryMBRList.add(strRecord);

                }while(allRCD.moveToNext());

            }
        }
        adtMembers = new ArrayAdapter<String>(this,
                android.R.layout.simple_list_item_single_choice, aryMBRList);

        lstView.setAdapter(adtMembers);
        lstView.setChoiceMode(ListView.CHOICE_MODE_SINGLE);
    }


    public boolean deleteTitle(String name)
    {
        return myDB.delete("Carlist", "CarType" + "=" + name, null) > 0;
    }

    public void onClick(View v) {

        myDB = this.openOrCreateDatabase("CarInformation", MODE_PRIVATE, null);

        if (v == btnInsert) {
            ContentValues insertNewValue = new ContentValues();
            insertNewValue.put("CarType", edtCarType.getText().toString());
            insertNewValue.put("CarPower", edtCarPower.getText().toString());
            myDB.insert("Carlist", null, insertNewValue);

            getDBData(null);
        }
        else if (v == btnUpdate) {
            strSQL = "Update Carlist Set ";
            strSQL += "CarType = " + "'" + edtCarType.getText().toString() + "', ";
            strSQL += "CarPower = " + "'" + edtCarPower.getText().toString() + "'";
            strSQL += "Where CarType = " + "'" + edtCarType.getText().toString() + "';";
            myDB.execSQL(strSQL);

            getDBData(null);

        }
        else if (v == btnDelete) {
            try {
                myDB.delete("Carlist", "CarType=? and CarPower=?", new String[]{edtCarType.getText().toString(), edtCarPower.getText().toString()});

                Cursor allRCD = myDB.query("Carlist", null, null, null, null, null, null, null);

                getDBData(null);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        else if (v == btnSearch) {
            strSQL = "CarType = '" + edtCarType.getText().toString() + "'";
            getDBData(strSQL);
        }
        else {
            getDBData(null);
        }
        if (myDB != null) myDB.close();
    }
}
```
