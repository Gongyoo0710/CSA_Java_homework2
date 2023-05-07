import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
public class homework2{
    public static int num = 0;
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("<-------第一题-------->");
        Monkey monkey = new Monkey("猴子");
        monkey.speak();
        People people = new People("人");
        people.speak();people.think();
        System.out.println("<-------第二题------->");
        Car car = new Car();
        car.wheels = 4;  car.weight = 1150.0F;
        Truck truck = new Truck();
        truck.wheels = 6;  truck.weight = 15000.0F;
        Wheel(car.wheels, car.weight);
        car.num(3);
        Wheel(truck.wheels, truck.weight);
        truck.num(1,3000);
        Wheel(car.wheels, car.weight);
        car.num(6);
        Wheel(truck.wheels, truck.weight);
        truck.num(1,7000);
        System.out.println("<-------第三题(大数相加)------->");
        System.out.println("请分别输入a,b");
        String a = scanner.next();
        String b = scanner.next();
        String c = getSum(a,b);
        System.out.println(c);
        System.out.println("<-------第四题（机器人路径）------->");
        int m,n;
        System.out.println("请分别输入m,n");
        m = scanner.nextInt();
        n = scanner.nextInt();
        int f = uniquePaths(m,n);
        System.out.println(f);
        System.out.println("<-------第五题（最大前缀）------->");
        String [] strs = new String[]{"flower", "flow", "flight"};
        System.out.println("'"+longestCommonPrefix(strs)+"'");
        String [] strs2 = new String[]{"dog","racecar","car"};
        System.out.println("'"+longestCommonPrefix(strs2)+"'");

    }
public static void Wheel(int wheel, float weight){
        System.out.println("车轮的个数   "+wheel+"  车重：  "+weight);
}

//TODO:在此编写作业所需的方法
//第三题格式要求 ,在TODO部分实现代码
public static String getSum(String a,String b){
        List<Integer> la = new ArrayList<Integer>();
        List<Integer> lb = new ArrayList<Integer>();
        String c = "";
        Boolean judge = false;
        int i;
        if(a.length() < b.length()){
            c = a; a = b; b = c;
        }
        c = "";
        for( i=a.length()-1;i>=0;--i){
           la.add(a.charAt(i)- '0');
       }
       for(i=b.length()-1;i>=0;--i){
           lb.add(b.charAt(i)- '0');
       }
       for(i=b.length(); i<a.length();i++){
           lb.add(0);
      }
       for(i = 0 ; i < a.length() ; i++){
           char ch ;
           if(la.get(i) + lb.get(i) <= 9)
               ch = (char) (la.get(i) + lb.get(i) +'0');
           else{
               ch = (char) (la.get(i) + lb.get(i) - 10 +'0');
               if(i < a.length()-1){
                   la.set(i+1,la.get(i+1)+1);}
               else{
                   judge = true;

               }
           }
           c += ch;
     }
       if(judge)
          c+='1';
       StringBuilder sb = new StringBuilder(c).reverse();
       c = sb.toString();
       return c;
  }

 //第四题格式要求
  public static int uniquePaths(int m, int n) {
        if(m==1||n==1){
            return 1;}
        else{
            return uniquePaths(m-1,n)+uniquePaths(m,n-1);}
        }
//第五题格式要求
   public static String longestCommonPrefix(String [] strs) {
       String ans = "";
       int i,MinLen = strs[0].length();
       String str = "";
       for(i = 0 ;i < strs.length;i++){
           if(strs[i].length()<MinLen)
               MinLen = strs[i].length();
       }
       outer:
       for( i = 0 ; i< MinLen;i++){
           for(int j = 0; j < strs.length; j++){
               str = strs[j].substring(0,i);
               if(!str.equals(ans)){
                   ans = ans.substring(0,ans.length()-1);
                   break outer;

               }
           }
           ans = strs[0].substring(0,i+1);
       }
      return ans;
   }}

class Monkey {
    private String name;
    public Monkey(String s){
        this.name = s;
    }
    public void speak(){
        System.out.println(name+"咿咿呀呀");
    }
}
class People extends Monkey{
    String name;

    public People(String s) {
        super(s);
        this.name =(s);
    }
    @Override
    public void speak(){
        System.out.println(name+"小样儿，不错嘛！会说话了！");
    }
    public void think(){
        System.out.println("别说话！认真思考！" );
    }
}

class Vehicle{
    int wheels;
    float weight;

}
class Car extends Vehicle{
    int loader = 5;
    public void num(int p){
    if(p>loader){
            System.out.println("这是一辆小车，能载"+loader+"人，实载"+p+'人');
    }else{
            System.out.println("这是一辆小车，能载"+loader+"人，实载"+p+"人，你超员了！！！");

    } }
}
class Truck extends Vehicle{
    int loader = 3;
    float payload = 5000;
    public void num(int p,float pay){
        if(p<loader){
            System.out.println("这是一辆小车，能载"+loader+"人，实载"+p+'人');
        }else{
            System.out.println("这是一辆小车，能载"+loader+"人，实载"+p+"人，你超员了！！！");
        }
        if(pay<payload){
            System.out.println("这是一辆卡车，核载"+payload+"kg,您已装载"+pay+"kg");
        }else{
            System.out.println("这是一辆卡车，核载"+payload+"kg,您已装载"+pay+"kg,你超载了!!!");
        }
    }
}
