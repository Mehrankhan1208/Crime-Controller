# Crime-Controller
splash screen

{

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_splash_screen);

    Thread thread = new Thread(){
      public void run(){
           try {
               sleep(3000);
           }
           catch (Exception e){
               e.printStackTrace();
           }
           finally {
               Intent intent = new Intent(Splash_screen.this , MainActivity.class);
               startActivity(intent);
           }
      }

    };thread.start();
}
}

//LOg in

<ImageView
    android:id="@+id/img1"
    android:layout_width="match_parent"
    android:layout_height="200sp"
    android:background="@drawable/background"

    />

<TextView
    android:id="@+id/tv1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:padding="10dp"
    android:layout_below="@id/img1"
    android:layout_centerHorizontal="true"
    android:text="Crime Controller"
    android:textSize="30sp" />

<EditText
    android:id="@+id/username1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/tv1"
    android:layout_centerHorizontal="true"
    android:hint="Enter email address"
    android:minHeight="48dp"
    android:padding="10dp" />

<EditText
    android:id="@+id/password1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/username1"
    android:layout_centerHorizontal="true"
    android:hint="Enter Password"
    android:minHeight="48dp"
    android:padding="10dp"
    android:textColor="@color/black" />


<TextView
    android:id="@+id/signup1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@+id/password1"
    android:layout_centerHorizontal="true"
    android:layout_marginStart="70sp"
    android:text="Don't have a account? Signup Here"
    android:textColor="#C6C6C6" />

<Button
    android:id="@+id/btnlogin1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/signup1"
    android:layout_centerHorizontal="true"
    android:hint="Log in"
    android:padding="10dp"
    android:textColor="@color/design_default_color_on_primary" />
package com.example.log_in;

import androidx.annotation.NonNull; import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent; import android.os.Bundle; import android.text.TextUtils; import android.view.View; import android.widget.Button; import android.widget.EditText; import android.widget.TextView; import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener; import com.google.android.gms.tasks.Task; import com.google.firebase.auth.AuthResult; import com.google.firebase.auth.FirebaseAuth; import com.google.firebase.auth.FirebaseUser;

public class log_in extends AppCompatActivity {

FirebaseAuth mAuth;
String email, password;
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_log_in);

    mAuth = FirebaseAuth.getInstance();

    EditText edtemail = findViewById(R.id.username1);
    EditText edtpass = findViewById(R.id.password1);
    TextView signup = findViewById(R.id.signup1);
    Button btnlogin = findViewById(R.id.btnlogin1);

    if (TextUtils.isEmpty(email)){
        edtemail.setError("Required");
    }
    if (TextUtils.isEmpty(password)){
        edtpass.setError("Required");
    }
    if (edtpass.length()<6){
        edtpass.setError("Minimum 6 characters required!");
    }

    btnlogin.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            email = edtemail.getText().toString().trim();
            password = edtpass.getText().toString();

            mAuth.signInWithEmailAndPassword(email, password).addOnCompleteListener(log_in.this, new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()){
                        FirebaseUser user = mAuth.getCurrentUser();
                        System.out.println(user);
                        Intent i = new Intent(getApplicationContext(),HomeActivity.class);
                        startActivity(i);
                    }else{
                        Toast.makeText(log_in.this, "Autehentication failed", Toast.LENGTH_SHORT).show();
                    }
                }
            });
        }
    });
    signup.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(getApplicationContext(),sign_up.class);
            startActivity(intent);
            finish();
        }
    });


}
}

Main Activity

<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" tools:context=".MainActivity">

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#222831"
    android:orientation="horizontal"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:orientation="vertical">


        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="20dp"
            android:layout_weight="0.5"
            android:orientation="horizontal">

            <LinearLayout
                android:id="@+id/scan"
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_margin="30dp"
                android:layout_weight="0.5"
                android:gravity="center"
                android:orientation="horizontal"
                android:padding="20dp">


                <Button
                    android:id="@+id/btnRegister"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:padding="20sp"
                    android:text="Register"
                     />

            </LinearLayout>

            <LinearLayout
                android:id="@+id/login"
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_margin="30dp"
                android:layout_weight="0.5"
                android:gravity="center">

                <Button
                    android:id="@+id/btnLogin"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Login"
                    android:padding="20sp"
                     />
            </LinearLayout>

        </LinearLayout>

        <TextView
            android:id="@+id/textView2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="No History!"
            android:textColor="#FFFFFF"
            android:textSize="16sp" />


        <androidx.recyclerview.widget.RecyclerView
            android:layout_width="match_parent"
            android:layout_height="match_parent" />

    </LinearLayout>

</LinearLayout>
</androidx.constraintlayout.widget.ConstraintLayout>

package com.example.log_in;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent; import android.os.Bundle; import android.view.View; import android.widget.Button; import android.widget.LinearLayout; import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
// LinearLayout scan = findViewById(R.id.scan); // LinearLayout login = findViewById(R.id.login); Button btnRegister = findViewById(R.id.btnRegister); Button btnLogin = findViewById(R.id.btnLogin);

    btnRegister.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            Intent in = new Intent(getApplicationContext(), sign_up.class);
            startActivity(in);
            Toast toast = Toast.makeText(getApplicationContext(), "Successfully", Toast.LENGTH_SHORT);
            toast.show();
        }
    });
    btnLogin.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent i = new Intent(getApplicationContext(), log_in.class);
            startActivity(i);
        }
    });

}
}

//Signup Activity

<ImageView
    android:id="@+id/img1"
    android:layout_width="match_parent"
    android:layout_height="200sp"
    android:background="@drawable/background"

    />


<TextView
android:id="@+id/tv"
android:layout_below="@id/img1"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:padding="20sp"
android:textSize="30sp"
android:layout_marginLeft="100sp"
android:text="Crime Controller"
/>

<EditText
    android:id="@+id/username"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@+id/tv"
    android:layout_centerHorizontal="true"
    android:hint="User name "
    android:minHeight="48dp"
    android:padding="10sp" />

<EditText
    android:id="@+id/et1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/username"
    android:layout_centerHorizontal="true"
    android:hint="Enter email address"
    android:minHeight="48dp"
    android:padding="10sp" />

<EditText
    android:id="@+id/password"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/et1"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="10sp"
    android:hint="Enter Password"
    android:minHeight="48dp"
    android:textColor="@color/black" />


<EditText
    android:id="@+id/repassword"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/password"
    android:layout_centerHorizontal="true"
    android:hint="Retype Password"
    android:minHeight="48dp"
    android:padding="10sp"
    android:textColor="@color/black" />

<Button
    android:id="@+id/btnsignin"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/repassword"
    android:layout_centerHorizontal="true"
    android:padding="10sp"
    android:hint="Register"
    android:textColor="@color/design_default_color_on_primary" />

<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:id="@+id/txtv"
    android:layout_below="@+id/btnsignin"
    android:layout_centerHorizontal="true"
    android:hint="Already Register? Login Here"></TextView>
package com.example.log_in;

import static android.content.ContentValues.TAG;

import androidx.annotation.NonNull; import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent; import android.net.nsd.NsdManager; import android.os.Bundle; import android.text.TextUtils; import android.util.Log; import android.view.View; import android.widget.Button; import android.widget.EditText; import android.widget.TextView; import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener; import com.google.android.gms.tasks.OnFailureListener; import com.google.android.gms.tasks.OnSuccessListener; import com.google.android.gms.tasks.Task; import com.google.firebase.auth.AuthResult; import com.google.firebase.auth.FirebaseAuth; import com.google.firebase.auth.FirebaseUser; import com.google.firebase.database.DatabaseReference; import com.google.firebase.database.FirebaseDatabase;

import org.w3c.dom.Text;

public class sign_up extends AppCompatActivity {

String name, email, password;
FirebaseAuth fAuth;
private DatabaseReference mDatabase;
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_sign_up);

    fAuth = FirebaseAuth.getInstance();

    EditText edtname = findViewById(R.id.username);
    EditText edtemail = findViewById(R.id.et1);
    EditText edtpassword = findViewById(R.id.password);
    EditText edtretypepassword = findViewById(R.id.repassword);
    Button btnregister = findViewById(R.id.btnsignin);
    TextView loginp = findViewById(R.id.txtv);
    mDatabase = FirebaseDatabase.getInstance().getReference();


    if (TextUtils.isEmpty(name)) {
        edtname.setError("Required");
    }
    if (TextUtils.isEmpty(email)) {
        edtemail.setError("Required");
    }
    if (TextUtils.isEmpty(password)) {
        edtpassword.setError("Required");
    }
    if (edtpassword.length() < 6) {
        edtpassword.setError("Enter minimum 6 characters");

    }
// if (fAuth.getCurrentUser() != null) { // startActivity(new Intent(getApplicationContext(), MainActivity.class)); // finish(); // }

    //Create user
    btnregister.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {

            name = edtname.getText().toString();
            email = edtemail.getText().toString().trim();
            password = edtpassword.getText().toString().trim();

            if (!edtname.getText().toString().isEmpty() && !edtemail.getText().toString().isEmpty() && !edtpassword.getText().toString().isEmpty()) {
                fAuth.createUserWithEmailAndPassword(email, password).addOnCompleteListener(sign_up.this, new OnCompleteListener<AuthResult>() {
                    private static final String TAG = "Registration";

                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if (task.isSuccessful()) {
                            FirebaseUser user = fAuth.getCurrentUser();
                            Log.d(TAG, "");
                            //to do add user into Real Time Database
                            mDatabase.child("users").child(user.getUid()).setValue(user).addOnSuccessListener(new OnSuccessListener<Void>() {
                                @Override
                                public void onSuccess(Void unused) {
                                    Toast.makeText(getApplicationContext(), "user added Successfully", Toast.LENGTH_SHORT).show();
                                }
                            }).addOnFailureListener(new OnFailureListener() {
                                @Override
                                public void onFailure(@NonNull Exception e) {
                                    Toast.makeText(getApplicationContext(), e.toString(), Toast.LENGTH_SHORT).show();

                                }
                            });
                            Intent i = new Intent(getApplicationContext(), MainActivity.class);
                            startActivity(i);
                        } else {
                            //To do if sign in fails, display a message to the user.
                            Toast.makeText(sign_up.this, task.getException().toString(), Toast.LENGTH_SHORT).show();
                        }
                    }
                });
            } else {
                Toast.makeText(getApplicationContext(), "Please fill all fields!", Toast.LENGTH_SHORT).show();
            }
        }
    });
    //Show login Screen
    loginp.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(getApplicationContext(),log_in.class);
            startActivity(intent);
            finish();
        }
    });

}
}
