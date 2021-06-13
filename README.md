# Broadcast-receiver-for-internet-connection-android
Check the internet connection with Broadcast receiver in Android


## step1:
  go to the AndroidManifest.xml and add this permissen.
  ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
## setep2:
  in the MainActivity.java or your Activity file and define a boolean value,for example :
  ```java
  boolean bb = true;
  ```
  ## step3:
  create a privet class in MainActivity.java or your Activity file and class extend from BroadcastReceiver,after creating the class,press the Alt and Enter keys to Override the class methods.
   ## step4:
   add these codes to the class
   ```java
       private class ConnectivityListener extends BroadcastReceiver{
        boolean isconnected;

        @Override
        public void onReceive(Context context, Intent intent) {
            ConnectivityManager connectivityManager =(ConnectivityManager)context.getSystemService(CONNECTIVITY_SERVICE);
            NetworkInfo networkInfo= connectivityManager.getActiveNetworkInfo();
            isconnected = networkInfo!=null && networkInfo.isConnectedOrConnecting();
            if (isconnected){
                bb=true;
            }else {
                bb=false;
            }

        }
    }
```
## step5:
create a variable of the class ConnectivityListener,like this
```java
public class MainActivity extends AppCompatActivity 
    boolean bb = true;

    private ConnectivityListener connectivityListener;
```
## step6:
in the MainActivity.java or your Activity file add onstart and onstop methods,like this
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

    }

    @Override
    protected void onStart() {
        super.onStart();
    }

    @Override
    protected void onStop() {
        super.onStop();
    }
}
```
## step7:
add these codes to the onstart and onstop methods:
```java
    @Override
    protected void onStart() {
        super.onStart();
        connectivityListener = new ConnectivityListener();
        registerReceiver(connectivityListener,new IntentFilter("android.net.conn.CONNECTIVITY_CHANGE"));
    }

    @Override
    protected void onStop() {
        unregisterReceiver(connectivityListener);
        super.onStop();
    }
```
### Extra tip
me for cheack internet connection create a Button and add set onclicklistener for Button.its codes are as follows
```java
        imageView4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (bb){
                    startActivity(new Intent(MainActivity.this,MediaActivity.class));
                }else {
                    Toast.makeText(MainActivity.this, "please cheack your connection Internet", Toast.LENGTH_SHORT).show();
                }

            }
        });
```
