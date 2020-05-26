```java
public class MyTest{
    public static void main(String[] args){
        double a = 12.81;
        int b = (int) a;
        System.out.println("强制类型转换" + b);
        
        long c = Math.round(a);
        System.out.println(c);
        
        int y = (int)(Math.random() * 99); // 返回[0，99）随机一个整数
        System.out.println(y);

        Random random = new Random();
        System.out.println(random.nextInt(99)); // 返回[0，99）随机一个整数
    }
}
```