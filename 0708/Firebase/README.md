# Android Studio Firebase연동

- Mobile, Web Application Development Platform
- NoSQL Cloud Real-time Database
- 실시간 연동
- 모든 클라이언트가 하나의 실시간 데이터베이스 인스턴스 공유
- 자동 업데이트로 최신 데이터 수신

### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/txtTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Customer Relationship Management"
        android:layout_marginStart="129dp"
        android:layout_marginTop="21dp"
        android:layout_marginEnd="126dp"
        android:gravity="center"
        android:textSize="18sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"/>

    <TextView
        android:id="@+id/txtName"
        android:layout_width="wrap_content"
        android:layout_height="19dp"
        android:text="Name: "
        android:layout_marginStart="16dp"
        android:layout_marginTop="90dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"/>

    <EditText
        android:id="@+id/edtCustomerName"
        android:layout_width="0dp"
        android:layout_height="48dp"
        android:ems="10"
        android:inputType="textPersonName"
        android:layout_marginStart="29dp"
        android:layout_marginTop="26dp"
        android:layout_marginEnd="13dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/txtName"
        app:layout_constraintTop_toBottomOf="@+id/txtTitle"/>

    <TextView
        android:id="@+id/txtPhoneNo"
        android:layout_width="73dp"
        android:layout_height="24dp"
        android:text="Phone_No: "
        android:layout_marginStart="12dp"
        android:layout_marginEnd="1dp"
        android:layout_marginBottom="14dp"
        app:layout_constraintTop_toBottomOf="@+id/txtName"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintBottom_toTopOf="@+id/btnInsert"
        app:layout_constraintEnd_toStartOf="@+id/edtCustomerPhoneNo"/>

    <EditText
        android:id="@+id/edtCustomerPhoneNo"
        android:layout_width="0dp"
        android:layout_height="48dp"
        android:ems="10"
        android:inputType="phone"
        android:layout_marginTop="81dp"
        android:layout_marginEnd="13dp"
        android:layout_marginBottom="81dp"
        app:layout_constraintBottom_toTopOf="@+id/txtFirebase"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/txtPhoneNo"
        app:layout_constraintTop_toBottomOf="@+id/txtTitle"
        tools:ignore="SpeakableTextPresentCheck"/>

    <Button
        android:id="@+id/btnInsert"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="Insert"
        android:layout_marginTop="20dp"
        android:layout_marginEnd="10dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/edtCustomerPhoneNo"/>

    <TextView
        android:id="@+id/txtFirebase"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginBottom="18dp"
        android:text="[ Firebase Value ]"
        android:layout_marginStart="11dp"
        android:layout_marginEnd="11dp"
        android:ems="10"
        android:gravity="start|top"
        android:inputType="textMultiLine"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/btnInsert"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

### MainActivity.java
```java
package com.inhatc.android_firebase3;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Debug;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.Query;
import com.google.firebase.database.ValueEventListener;

import java.util.HashMap;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    FirebaseDatabase myFirebase;
    DatabaseReference myDB_Reference = null;

    TextView txtFirebase;
    EditText edtCustomerName, edtCustomerPhoneNo;
    Button btnInsert;
    String strHeader = "Customer Information";
    String strCName = null;
    String strCPhoneNo = null;
    HashMap<String, Object> Customer_Value = null;
    CustomerInfo objCustomerInfo = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        txtFirebase = (TextView) findViewById(R.id.txtFirebase);
        edtCustomerName = (EditText) findViewById(R.id.edtCustomerName);
        edtCustomerPhoneNo = (EditText) findViewById(R.id.edtCustomerPhoneNo);

        btnInsert = (Button) findViewById(R.id.btnInsert);
        btnInsert.setOnClickListener(this);

        myFirebase = FirebaseDatabase.getInstance();
        myDB_Reference = myFirebase.getReference();
        Customer_Value = new HashMap<>();

    }

    @Override
    public void onClick(View view) {
        switch (view.getId()) {
            case R.id.btnInsert:
                strCName = edtCustomerName.getText().toString();
                strCPhoneNo = edtCustomerPhoneNo.getText().toString();

                if (!strCName.equals("") & !strCPhoneNo.equals("")) {
                    mSet_FirebaseDatabase(true);
                    mGet_FirebaseDatabase();
                }
                edtCustomerName.setText("");
                edtCustomerPhoneNo.setText("");
                break;
            default:
                edtCustomerName.setText("");
                edtCustomerPhoneNo.setText("");
                break;
        }
    }

    private void mSet_FirebaseDatabase(boolean bFlag) {
        if (bFlag) {
            Customer_Value.put("Name", strCName);
            Customer_Value.put("Phone_No", strCPhoneNo);
            myDB_Reference.child(strHeader).child(strCPhoneNo).setValue(Customer_Value);

        }
    }

    private void mGet_FirebaseDatabase() {
        ValueEventListener postListener = new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot datasnapshot) {
                txtFirebase.setText("[ Firebase Value ]");
                int iCnt = 0;
                for (DataSnapshot postSnapshot: datasnapshot.getChildren()) {
                    iCnt++;
                    String strKey = postSnapshot.getKey();
                    String strValue = postSnapshot.getValue().toString();
                    txtFirebase.append("\n " + "\t" + iCnt +" : " + strKey);
                    txtFirebase.append("\n " + "\t = " + strValue);

                }
            }

            @Override
            public void onCancelled(@NonNull DatabaseError dbError) {
                Log.w("Tag: ", "Failed to read value", dbError.toException());
            }
        };

        Query sortbyName = FirebaseDatabase.getInstance().getReference().child(strHeader).orderByChild(strCName);
        sortbyName.addListenerForSingleValueEvent(postListener);
    }

}
```
