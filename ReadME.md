## 부분 배낭 문제 : 이종웅

```
import java.util.Arrays;
import java.util.Comparator;

public class Leejongwoong {
    public static double woong(int[] w, int[] v, int c) {
        temval[] V = new temval[w.length];
        for (int i = 0; i < w.length; i++) {
            V[i] = new temval(w[i], v[i], i); }
        Arrays.sort(V, new Comparator<temval>() {
            public int compare(temval o1, temval o2) {
                return o2.a.compareTo(o1.a); }});
        double tv = 0;

        for (temval i : V) {
            int wt = (int) i.w;
            int vl = (int) i.v;
            if (c - wt >= 0) {
                c = c - wt;
                tv += vl;
            } else {
                double f = ((double) c / (double) wt);
                tv += (vl * f);
                c = (int) (c - (wt * f));
                break; }
        }
        return tv;
    }

    static class temval {
        Double a;
        double w, v, i2;

        public temval(int w, int v, int i2) {
            this.w = w;
            this.v = v;
            this.i2 = i2;
            a = new Double((double) v / (double) w);

        }
    }
    public static void main(String[] args) {
        int[] w = {10, 20, 30, 40};
        int[] v = {20, 50, 100, 120};
        int c = 50;

        double maxv = woong(w, v, c);
        System.out.print("배낭에 담을 수 있는 최대 물건의 최대 가치 = "
                + maxv);
    }
}
```

# greed2


#### 팀원: 강현규, 류연수, 이종웅
---


### 코드설명  

```import java.util.Arrays;
import java.util.Comparator;
```
> 배열을 다루기 위해 `util.java.` 패키지에서 `Arrays` 클래스를 불러온다.  
> Arrays.sort() 메소드의 기준으로 삽입해줄 정렬 기준을 가진 `Comparator` 클래스도 불러온다.
---

```Java
public class Leejongwoong {
    public static double woong(int[] w, int[] v, int c) {
        temval[] V = new temval[w.length];
        for (int i = 0; i < w.length; i++) {
            V[i] = new temval(w[i], v[i], i); }
        Arrays.sort(V, new Comparator<temval>() {
            public int compare(temval o1, temval o2) {
                return o2.a.compareTo(o1.a); }});
        double tv = 0;
```
>`temval`의 최대값을 구하고 `a`의 무게와 가치를 비교하여 내림차순으로 정렬한다.  
---

```Java
        for (temval i : V) {
            int wt = (int) i.w;
            int vl = (int) i.v;
            if (c - wt >= 0) {
                c = c - wt;
                tv += vl;
            } else {
                double f = ((double) c / (double) wt);
                tv += (vl * f);
                c = (int) (c - (wt * f));
                break; }
        }
        return tv;
    }
```
>` int[] w = { 10, 20, 30, 40 }; int[] v = { 20, 50, 100, 120 };`에서의 최대 가치 `w 40, v 120`을 먼저 배낭에 넣은 뒤 10만큼의 남은 무게를 물건들의 무게와 가치를 비교하여 무게가 초과된다면 무게와 가치를 비례해 줄여 `c`의 값인 50에 맞춰 배낭에 넣어준다.  
>`c(배낭 안에 들어갈 수 있는 최대 무게)`의 값에서 `wt(물건들의 무게)`뺀 값이 0보다 크거나 같으면(0이라면) `c = c - wt;`이며,
>`tv`의 값은 `w`의 `v(물건들의 가치)`이다.
>`c - wt`의 값이 0보다 작다면(물건들의 무게가 배낭에 넣을 수 있는 무게를 초과한다면) 초과하는 물건들 중에서
>`c - wt`가 0가 되도록 가치가 높은 물건의 물건의 무게와 가치를 비례하여 줄여 `tv`에 저장해준 뒤 리턴해준다.
---

```Java
   static class temval {
        Double a;
        double w, v, i2;

        public temval(int w, int v, int i2) {
            this.w = w;
            this.v = v;
            this.i2 = i2;
            a = new Double((double) v / (double) w);

        }
    }
    public static void main(String[] args) {
        int[] w = {10, 40, 20, 30};
        int[] v = {60, 40, 100, 120};
        int c = 50;
```
>`temval`의 함수 `a = new Double((double)v / (double)w);`를 통해 `w(무게)`와 `v(가치)`를 비교하여  `public class Leejongwoong Comparator`정렬에서 내림차순으로 정렬을 한다.
>`main` 함수에서 `w(물건들 무게)`와 `v(물건들 가치)`, `c(배낭의 들어갈 수 있는 최대 무게)`의 값을 정하였다.
---

```Java
        double maxValue = woong(w, v, c);
        System.out.print("배낭에 담을 수 있는 최대 물건의 최대 가치 = "
                + maxValue);
    }
}

```
>`woong`함수를 호출하여 `maxv`에 저장 후 `print`해준다.
>이 때 `woong`함수는 `Comparator a`함수에 의해서 내림차순으로 된 물건들을 `for`문으로 인해 가치가 가장 큰 값을 먼저 배낭에 넣어준 뒤 나머지 무게에 대해 무게와 가치를 비교하여 가장 높은 가치의 물건을 `c` 값 50에 맞춰서 넣어준다.
---

### 결과값

>배낭에 담을 수 있는 최대 물건의 최대 가치 = 160.0

---

------------------------------------------------------------------------------------------------------------------------------------------------

## 부분 배낭 문제 : 강현구

전체 코드

```
import java.util.*;
import java.util.stream.Collectors;


class object{
    String name;
    int weight;
    int value;

    public object(String name, int weight, int value){
        this.name = name;
        this.weight = weight;
        this.value = value;
    }
}


public class FractionalKanpsack {
    public static void main(String[] args){
        int C = 40;
        int v = 0;
        int w = 0;

        List<object> L =  new ArrayList<object>();
        List<object> S = new ArrayList<object>();   //물건 리스트

        S.add(0, new object("주석", 50, 50000));
        S.add(1, new object("백금", 10, 600000));
        S.add(2, new object("은", 25, 100000));
        S.add(3, new object("금", 15, 750000));

        S = S.stream().sorted((object a, object b) -> {    //무게당 가치 순으로 내림차순 정렬
            int A = a.value/a.weight;
            int B = b.value/b.weight;
            if(A<B) return 1;
            else if (A==B) return 0;
            else return -1;
        }).collect(Collectors.toList());

        System.out.println();

        int k = 0;
        int x = S.get(0).weight;
        while(w+x <= C){  //0+10(백금의무게) <= 40 true  -> 10+15(금의 무게) <=40 true
            L.add(k, S.get(0)); //L에 S(0)(백금) 추가    -> 반복
            w+=L.get(k).weight; //w = w+10
            v+=L.get(k).value;  //v = v+60
            S.remove(0);    //S(0) 백금 삭제
            k++;    //L의 인덱스만 증가 (S의 0번 인덱스를 삭제하면 1번 인덱스가 0번인덱스로 된다.)
            x = S.get(0).weight;
        }

        if((C-w) > 0){  //배낭에 물건을 부분적으로 담을 여유 있다면
            L.add(k,new object(S.get(0).name, C-w, ((S.get(0).value/S.get(0).weight)*(C-w))));
            w+=(C-w);
            v+=L.get(k).value;
        }
        for(int i=0; i<L.size(); i++){
            System.out.print(L.get(i).name + L.get(i).weight + "g" + " ");
        }
        System.out.println();
        System.out.println("w=" + w + "g");
        System.out.println("v=" + v + "원");
    }
}

```



코드를 짜는중 물건들을 무게당 가치순으로 내림차순 정렬하는 부분에서 어려움을 겪었다. 처음엔 리스트를 무게당 가치를 기준으로 정렬하는 것에서 혼란을 겪었지만, 검색을 통해서 리스트를 정렬하는 메소드를 알게되었고, 밑의 코드처럼 사용자가 자신의 비교기를 작성할 수도 있다는 사실도 알게되었다.

<img src="C:\Users\82104\Desktop\오류 1.PNG" style="zoom:80%;" />

![오류](C:\Users\82104\Desktop\오류 2.PNG)

위 사진은 백금과 금까지는 정렬이 정상적으로 되었지만, 주석과 은이 반대로 정렬되는 모습이다. 이를 왜그럴까 생각해보니 무게당 가치(v/w)을 계산한 값이 정수가 아닌 값(0.1과 0.4)이 나와서 그랬을 것이라고 생각해 object의 value값에 10,000을 곱해서 코드를 수정했다.

<img src="C:\Users\82104\Desktop\해결 1.PNG" style="zoom:80%;" />

![해결](C:\Users\82104\Desktop\해결 2.PNG)

그러면 위 사진처럼 정상적으로 정렬되는걸 확인 할 수 있었다.

 다음으로 물건을 쪼개서 가방에 담는 코드 부분이다.

![](C:\Users\82104\Desktop\쪼개서넣기.PNG)



기존에 L리스트에 담겨있는 은을 쪼개는 것엔 한계를 느끼고 대신에 은 15g 만큼의 새로운 object를 만들어 L리스트에 추가했다.
이렇게 해서 마지막 리스트 L과 가치의 합 v의 결과는 이렇게 나온다.

![](C:\Users\82104\Desktop\결과.PNG)

## 부분 배낭 문제 : 류연수

## Greedy algorithm

### problem : Knapsack fractional

전체적인 코드는 다음과 같다.

```
import java.util.Scanner;

public class Knapsack {
    private int weight;
    private int price;
    private int cost;

    public Knapsack(int w, int p) {
        super();

        this.weight = w;
        this.price = p;
        this.cost = (p/w);
    }

    public int GetWeight() {
        return weight;
    }

    public int GetPrice() {
        return price;
    }

    public int GetCost() {
        return cost;
    }

    public static Knapsack[] sort(Knapsack [] kp) {
        int max = 0;
        Knapsack change = new Knapsack(0, 0);

        for (int i = 0; i < kp.length - 1; i++) {
            max = kp[i].cost;
            for (int j = i + 1; j < kp.length; j++) {
                if (max < kp[j].cost) {
                    change.weight = kp[i].weight;
                    change.price = kp[i].price;
                    change.cost = kp[i].cost;

                    kp[i].weight = kp[j].weight;
                    kp[i].price = kp[j].price;
                    kp[i].cost = kp[j].cost;

                    kp[j].weight = change.weight;
                    kp[i].price = change.price;
                    kp[i].cost = change.cost;

                    max = kp[j].cost;
                }
            }
        }
        return kp;
    }

    public static void KnapsackPerform(int w[], int p[],int c, int size) {
        Knapsack [] kp = new Knapsack[size];

        for(int i = 0; i<kp.length;i++) {
            kp[i] = new Knapsack(w[i], p[i]); 
            //총 금액, 량, 단위 당 금액을 가지고 있는 클래스형 배열 생성
        }

        kp = sort(kp); //단위 당 금액을 기준으로 배열 정렬 시키는 함수

        Knapsack [] result = new Knapsack[size];

        int current_w = 0;
        int current_v = 0;

        for(int i = 0; i < kp.length; i++) {
            if(c >= current_w + kp[i].weight) {
                current_w += kp[i].GetWeight();
                current_v += kp[i].GetPrice();
                result[i].weight = kp[i].GetWeight();
                result[i].price = kp[i].GetPrice();
            }
            else if(c - current_w > 0) {
                current_w += c - current_w;
                current_v += (c - current_w)*kp[i].GetCost();
                result[i].weight = (c - current_w);
                result[i].price = (c - current_w)*kp[i].GetCost();
            }
        }

        System.out.println("최종 weight 와 price : " + current_w + " , " + current_v);
        for(int i = 0; i < result.length; i++) {
            System.out.println( i + " " + result[i].weight + " " + result[i].price);
        }
    }

    public static void main(String [] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("총 대상의 개수 : ");
        int number = scanner.nextInt();

        int arr_w[] = new int [number];
        int arr_p[] = new int [number];

        System.out.println("대상들의 weight : ");

        for(int i = 0; i < number; i++) {
            arr_w[i] = scanner.nextInt();
        }

        System.out.println("대상들의 price : ");
        for(int i = 0; i < number; i++) {
            arr_p[i] = scanner.nextInt();
        }

        System.out.println("수용량 입력 : ");
        int capacity = scanner.nextInt();

        KnapsackPerform(arr_w,arr_p,capacity, number);
    }
}

```

-------------

#### class 설명

1. class Knapsack는 weight, price, cost에 대한 멤버변수를 가지며, 매개변수가 2개인 메서드를 가지고 있다.
2. 메서드는 입력받은 w, p를 해당 객체의 멤버변수 weight, price에 넣고 매개변수에 간단한 사칙연산을 취해 구한 cost의 값까지 대입해주는 역할을 한다. 
3. 각 GetWeight(), GetPrice(), GetCost()는 객체에 대해 얻고자 하는 값을 간단하게 가져오는 함수라 보면 된다. 



#### 함수 설명

구현한 함수 : KnapsackPerform(), sort() 

1. **KnapsackPerform() :**

(1) 입력받은 값들을 기준으로 **클래스형 배열**에 정보를 할당해주고

(2) 만들어진 배열을 sort함수에 보내 정렬시켜준다.

(3) 결과적으로 선택된 대상들의 양과 금액을 저장할 배열을 만들고

(4) 수용량을 기준으로 **최대한 높은 단위 당 값어치**를 가질 수 있도록 대상들을 선별.

(5) 최종적으로 선택된 무게와 총 값어치, 대상들에 대한 정보를 출력하는 함수이다. 



2. **sort() :** 

(1) 만들어진 클래스형 배열을 매개변수로 받는다

(2) 현재 가장 첫 번째 인덱스에 들어가있는 cost 값이 **가장 큰 값이라 가정**하고 for문을 진행한다.

(3) for문을 진행하는 과정에서 max값 보다 큰 값이 있다면 그 값으로 정보를 change해준다.

(4) 첫 번째 요소부터 마지막 요소까지 모두 이 과정을 거쳐 **내림차순**으로 배열을 정렬하여 반환하는 함수.

