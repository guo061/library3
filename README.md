# library3
效果截图：![C8VL}`D%)_F$UZ`I6)8B1)R](https://user-images.githubusercontent.com/114241292/201456091-8b670331-fdad-4a0c-a7fe-ce91128a919a.png)
代码：
  （1）Exam3Activity.java
  首先是设置一个简单的框架，再设置toast，toast显示列表项信息，选中哪个便显示name的position，其中包括选中后背景颜色的改变以及不被选中时背景颜色的恢复。
  public class Exam3Activity extends AppCompatActivity {
    private String[] names = new String[]{"Lion","Tiger","Monkey","Dog","Cat","elephant"};
    private int[] image=new int[]{R.drawable.lion,R.drawable.tiger,R.drawable.monkey,R.drawable.dog,R.drawable.cat,R.drawable.elephant};
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.main);//此处引用~~~~~
        final int color1=0xFFC5B5FF;
        final int color2=0xFFFFFFFF;
        //创建一个list集合，list集合的元素是Map
        List<Map<String,Object>> ListItems=new ArrayList<Map<String, Object>>();
        for (int i=0;i<names.length;i++){
            Map<String,Object> listItem=new HashMap<String,Object>();
            listItem.put("header",names[i]);
            listItem.put("images",image[i]);
            ListItems.add(listItem);//加入list集合
        }
        //创建一个SimpleAdapter
        SimpleAdapter simpleAdapter=new SimpleAdapter(this,ListItems,R.layout.simple_items,new String[]{"header","images"},new int[]{R.id.header,R.id.images});
        final ListView list=(ListView)findViewById(R.id.mylist);
        //为ListView设置Adapter
        list.setAdapter(simpleAdapter);
        list.setOnItemClickListener(new AdapterView.OnItemClickListener(){
            public void onItemClick(AdapterView<?> parent, View view, int position, long id){
                int flag=0;
                System.out.println(names[position]+position+"被单击");
                switch (flag){
                    case 0:
//                        view.setBackgroundColor(color1);
                        view.setSelected(true);
                        CharSequence text=names[position];
                        int duration= Toast.LENGTH_SHORT;
                        Toast toast=Toast .makeText(Exam3Activity.this,text,duration);
                        toast.show();
                        flag=1;
                        break;
                    case 1:
//                        view.setBackgroundColor(color2);
                        view.setSelected(false);
                        CharSequence text1=names[position];
                        int duration1= Toast.LENGTH_SHORT;
                        Toast toast1=Toast .makeText(Exam3Activity.this,text1,duration1);
                        toast1.show();
                        flag=0;
                        break;
                }
            }
        });
        list.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener(){
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id){
                System.out.println(names[position]+"选中");
            }
            public void onNothingSelected(AdapterView<?> parent){

            }
        });
    }

}

  （2）simple_items.xml
  <LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal">
    <TextView
        android:id="@+id/header"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textColor="#000000"
        android:textSize="20dp"
        android:paddingLeft="10dp"
        />
    <RelativeLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">
        <ImageView
            android:id="@+id/images"
            android:layout_width="50dp"
            android:layout_height="50dp"
            android:layout_margin="0dp"
            android:layout_alignParentRight="true"
            />
    </RelativeLayout>
</LinearLayout>
加上颜色渲染等处理后的效果图：
  ![CH0XTC)VHED5YQ 3NY2M61O](https://user-images.githubusercontent.com/114241292/201456453-1754c233-e061-479e-aced-86dc8f8686b2.png)
