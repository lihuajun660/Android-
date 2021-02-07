### 10.2.2
============

1）Android的UI也是线程不安全的，不允许在子线程中进行UI操作。
2）使用异步消息处理来解决子线程中进行UI操作的问题。

``` java
public class MainActivity extends AppCompatActivity implements View.OnClickListener{

    public static final int UPDATE_TEXT = 1;

    private TextView text;

    private Handler handler = new Handler(){
        @Override
        public void handleMessage(@NonNull Message msg) {
            switch (msg.what){
                case UPDATE_TEXT:
                    //在这里进行UI操作
                    text.setText("Nice to meet you");
                    break;
                default:
                    break;
            }
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        text = (TextView) findViewById(R.id.text);
        Button changeText = (Button) findViewById(R.id.change_text);
        changeText.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()){
            case R.id.change_text:
                new Thread(new Runnable() {
                    @Override
                    public void run() {
                        Message message = new Message();
                        message.what = UPDATE_TEXT;
                        handler.sendMessage(message); //将message对象传送过去
                    }
                }).start();
                break;
            default:
                break;
        }
    }
}
```

10.2.3  解析异步消息处理机制
=================
#1. Message
-----------
Message是在线程之间传递的消息，它可以在内部携带少量的信息，用于在不同线程之间交互数据。

#2. Handler
-----------
用于发送和处理信息 sendMessage()方法  ----->  handleMessage()方法

#3. MessageQueue
-----------
每个线程中，只会有一个MessageQueue对象

#4. Looper
-----------
是MessageQueue的管家，调用looper的loop()方法后，就会进入到一个无限循环中，然后每当发现MessageQueue中存在一条信息，就会将它取出，并传递到Handler的handleMessage()方法中，每个线程也只会有一个线程对象。
*一句话：会一直尝试从MessageQueue中取出待处理消息，最后分发回Handler的handleMessage()方法中*

10.2.4 使用AsyncTask
==========
抽象类，3个 **泛型** 参数
* Params
* Progress  在界面上显示当期的进度
* Result

1. onPreExcute()
2. doInBackground(Params ...)  ----->  执行具体的耗时任务
3. onProgressUpdate(Progress...)  ----->  进行UI操作
4. onPostExcute(Result)   ------>  执行一些任务的收尾工作

启动这个任务：
new downloadTash(). excute();


10.3 服务的基本用法
=====================

onBind()是继承自Service类的，说明这是一个服务。onBind()方法是service中唯一的一个抽象方法，所以必须在子类中实现。

服务中最常用到的三个方法
```
    @Override
    public void onCreate() {
        super.onCreate();
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
    }
```

10.4 服务的生命周期
==================
启动：startService()---> [onCreate()]  -----> onStartCommand()  
结束：stopService() / stopSelf()




















