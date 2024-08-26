---
layout: single
title:   "네이버와 구글도 따라하는 HTML 문서 기본 구조"
categories: HTML
toc : true
author_profile : false
---

# 생성자 왜 필요함?
얼마전 스타벅스를 갔다. 스벅에 가면 늘 점원이 같은 걸 물어본다

> 뭐드실?
> 차가운거 따뜻한거?
> 주차하심?
> 프리퀀시?
> 
> 1. 아이스 아메리카노 맞으시져?
> 2. 주차 2시간 입력해드렸어요~
> 3. 프리퀀시 적립해드렸어요~

점원은 이것을 무한 반복한다.
이 과정이 이뤄지는데 짧으면 30초, 길면 3분 정도가 소요되기도한다.
완벽한 **절차 지향적 방식**이다.

손님 1명당 평균 1분 30초라 가정하고, 하루 500잔 정도를 팔면 12.5시간이 주문 받는데만 소요된다.

코드로 치면 아래와 같다.

> 참고
> 여기서 **Main**이 들어간 부분만 **점원이 해야할 일**이다.

**OrderCoffeeMain1**
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner order = new Scanner(System.in);

        System.out.print("뭐 드실?: ");
        String coffee = order.nextLine();

        System.out.print("차가운거? 따뜻한거?: ");
        String choice = order.nextLine();

        System.out.print("주차 하심?('yes' or 'no'): ");
        String parking = order.nextLine();

        System.out.print("프리퀀시 적립?('yes' or 'no'): ");
        String frequency = order.nextLine();

        System.out.println("주문내역");
        System.out.println("1. coffe: " + choice + coffee);
        System.out.println("2. parking: " + parking);
        if (parking.equals("yes")) {
            System.out.println("2시간 무료 주차 쿠폰이 적용되었습니다.");
        }
        System.out.println("3. frequency: " + frequency);
        if (frequency.equals("yes")) {
            System.out.println("프리퀀시 1개가 적립되었습니다.");
        }
    }
}
```

**실행결과**
```java
뭐 드실?: americano
차가운거? 따뜻한거?: ice
주차 하심?('yes' or 'no'): yes
프리퀀시 적립?('yes' or 'no'): yes
주문내역
1. coffe: iceamericano
2. parking: yes
2시간 무료 주차 쿠폰이 적용되었습니다.
3. frequency: yes
프리퀀시 1개가 적립되었습니다.
```

자, 여러분이 사장이라면 점원의 낭비되는 시간을 없애고 좀 더 수월하게 커피를 만들 수 있게하려면 어떻게하는게 좋을까?

![](https://velog.velcdn.com/images/evansong/post/e34a32a0-7ca4-49ca-972c-bb33a413c2fd/image.png)출처: 라이프타임 채널 ‘하프 홀리데이’

나의 첫번째 아이디어는 점원이 **질문하는 방법**만 알면 필요한 정보가 무엇인지 몰라도 소비자가 원하는 정보를 줄 수 있게 해주는 것이다.

---

### step.1 점원이 질문하는 법만 알면 나머지는 알아서 해주자.

> ex)
- 주문에 필요한 정보
  - 커피종류, 타입(ice or hot), 주차, 프리퀀시
- 질문하는 법
  - 커피 종류: "뭐 드실?"

따라서, 질문하는 방법에 대한 양식을 정리한 **업무 바인더**를 만들었다.

**OrderCoffee2**
```java
import java.util.Scanner;

public class OrderCoffee2 {
    Scanner order = new Scanner(System.in);
    public String coffee;
    public String type;
    public String parking;
    public String frequency;

    public void orderCoffee() {
        System.out.print("뭐 드실?: ");
        this.coffee = order.nextLine();
    }

    public void choiceCoffeeType() {
        System.out.print("차가운거? 따뜻한거?: ");
        this.type = order.nextLine();
    }

    public void parkingValidated() {
        System.out.print("주차 하심?('yes' or 'no'): ");
        this.parking = order.nextLine();
    }

    public void getFrequency() {
        System.out.print("프리퀀시 적립?('yes' or 'no'): ");
        this.frequency = order.nextLine();
    }

    public void printReceipt(OrderCoffee2 order) {
        System.out.println("1. coffee: " + order.type + " " + order.coffee);
        System.out.println("2. parking: " + order.parking);
        if (order.parking.equals("yes")) {
            System.out.println("2시간 무료 주차 쿠폰이 적용되었습니다.");
        }
        System.out.println("3. frequency: " + order.frequency);
        if (order.frequency.equals("yes")) {
            System.out.println("프리퀀시 1개가 적립되었습니다.");
        }
    }
}
```


이제 직원은 업무바인더에 적힌대로 주문서에 필요한 질문을 소비자에게 하고, 프린트 버튼을 통해 주문내역을 출력해줄 수 있다.

**OrderCoffeeMain2**
```java
import java.util.Scanner;

public class OrderCoffeeMain2 {
    public static void main(String[] args) {
        Scanner order = new Scanner(System.in);
        OrderCoffee2 orderCoffee = new OrderCoffee2();

        // 커피 주문서
        orderCoffee.orderCoffee();
        // 타입 주문서
        orderCoffee.choiceCoffeeType();
        // 주차 여부
        orderCoffee.parkingValidated();
        // 프리퀀시 적립 여부
        orderCoffee.getFrequency();
        // 주문내역 프린트
        orderCoffee.printReceipt(orderCoffee);
    }
}
```


**실행결과**
  ```java
뭐 드실?: americano
차가운거? 따뜻한거?: ice
주차 하심?('yes' or 'no'): yes
프리퀀시 적립?('yes' or 'no'): yes
1. coffee: ice americano
2. parking: yes
2시간 무료 주차 쿠폰이 적용되었습니다.
3. frequency: yes
프리퀀시 1개가 적립되었습니다.
  ```
  
이제 직원은 각각의 **질문지가 적힌 주문서를 건네주기**만 하면된다.
소비자가 해당 주문서를 읽어보고 질문에 대한 답을 적어내면, 직원은 그저 프린트 버튼만 누르면 된다.

그러나 사장인 당신은 여기서도 비효율을 발견하게된다.

위에서 본 주문서들은 모두 **하나의 커피주문**을 처리하기 위해 작성되야하는 정보들이다.

이걸 한번에 처리할 순 없을까?
![](https://velog.velcdn.com/images/evansong/post/baf8623a-fce8-4e3c-8bb2-5f9a42c73a9b/image.png)출처: 라이프타임 채널 ‘하프 홀리데이’

---
  
  ### step2. 점원이 질문할 필요도 없게 해주자.

> 손님과 점원이 마주하면 다음과 같은 상황이 펼쳐진다.
> 1. 직원이 손님에게 커피 주문 양식을 건넨다.
> 2. 손님이 해당 양식을 작성한다.
> 3. 주문 내역서가 자동으로 손님에게 전달된다.

**OrderCoffee3**
```java
import java.util.Scanner;

public class OrderCoffee3 {
    Scanner order = new Scanner(System.in);
    public String coffee;
    public String type;
    public String parking;
    public String frequency;

    public OrderCoffee3() {
        orderCoffee();
        choiceCoffeeType();
        parkingValidated();
        getFrequency();
        printReceipt(this);

    }
    public void orderCoffee() {
        System.out.print("뭐 드실?: ");
        this.coffee = order.nextLine();
    }

    public void choiceCoffeeType() {
        System.out.print("차가운거? 따뜻한거?: ");
        this.type = order.nextLine();
    }

    public void parkingValidated() {
        System.out.print("주차 하심?('yes' or 'no'): ");
        this.parking = order.nextLine();
    }

    public void getFrequency() {
        System.out.print("프리퀀시 적립?('yes' or 'no'): ");
        this.frequency = order.nextLine();
    }

    public void printReceipt(OrderCoffee3 orderCoffee3) {
        System.out.println("1. coffee: " + orderCoffee3.type + " " + orderCoffee3.coffee);
        System.out.println("2. parking: " + orderCoffee3.parking);
        if (orderCoffee3.parking.equals("yes")) {
            System.out.println("2시간 무료 주차 쿠폰이 적용되었습니다.");
        }
        System.out.println("3. frequency: " + orderCoffee3.frequency);
        if (orderCoffee3.frequency.equals("yes")) {
            System.out.println("프리퀀시 1개가 적립되었습니다.");
        }
    }
}
```

**OrderCoffeeMain3**
```java
public class OrderCoffeeMain3 {
    public static void main(String[] args) {
        OrderCoffee3 orderCoffee = new OrderCoffee3();
    }
}
```

**실행 결과**
```java
뭐 드실?: americano
차가운거? 따뜻한거?: ice
주차 하심?('yes' or 'no'): yes
프리퀀시 적립?('yes' or 'no'): yes
1. coffee: ice americano
2. parking: yes
2시간 무료 주차 쿠폰이 적용되었습니다.
3. frequency: yes
프리퀀시 1개가 적립되었습니다.
```

결과는 똑같다. 그러나 이제 점원은 그저 주문서를 건네주면 알아서 주문 내역서가 고객에게 전달된다.

이게 가능한 이유가 바로 **생성자** 덕분이다.

즉, ```OrderCoffee```라는 인터페이스를 생성함과 동시에 해당 인터페이스가 가지고 있는 정보들과 필요한 정보들을 사용자에게 함께 호출하기 때문이다.

이렇게 생성자를 사용하면 해당 상황이 펼쳐질 때 필요한 멤버변수와 메서드들이 함께 호출되기 때문에 보다 간편하고 쉽게 프로그램 활용이 가능해진다.

다시말해, 사용자는 프로그램을 사용하기만 하면된다. 사용하기 위해 자세한 내용까지는 몰라도 된다는 뜻이다.

이렇게 **역할과 구현**을 구분해 놓는것.
이것이 객체 지향 프로그래밍의 기본이고 생성자는 바로 그런 역할을 도와준다.

### 번외. 주문 내역서를 자기가 직접 바꿔치기하는 도둑놈이 있다면?

> 매 주문마다 손님에게는 정확한 주문내역서가 나갔다.
> 그런데 종업원 **김횡령**은 일부러 손님이 주문한 커피보다 싼 커피로 주문서를 바꿔치기했다.
> 그리고 남은 돈을 몰래 횡령하고 있었다.

![](https://velog.velcdn.com/images/evansong/post/ed295c46-2e23-4b16-bd1c-0fd55fbf28d5/image.png)



**EmbezzlementMain**
```java
public class OrderCoffeeMain4 {
    public static void main(String[] args) {
        OrderCoffee4 orderCoffee = new OrderCoffee4();
        
        //김횡령의 횡령 정황
        orderCoffee.coffee = "esspresso";
        orderCoffee.type = "hot";
        orderCoffee.parking = "no";
        orderCoffee.frequency = "no";
        
        // 사장인 당신이 확인한 결과
        System.out.println(orderCoffee.coffee);
        System.out.println(orderCoffee.type);
        System.out.println(orderCoffee.parking);
        System.out.println(orderCoffee.frequency);
    }
}
```

**실행결과**
```java
뭐 드실?: ameircano
차가운거? 따뜻한거?: ice
주차 하심?('yes' or 'no'): yes
프리퀀시 적립?('yes' or 'no'): yes
1. coffee: ice ameircano
2. parking: yes
2시가 무료 주차 쿠폰이 적용되었습니다.
3. frequency: yes
프리퀀시 1개가 적립되었습니다.
esspresso
hot
no
no
```

이러한 횡령을 막기 위해서는 외부에서 주문서를 조작할 위험을 애초에 없애야한다.

어떻게 할 수 있을까?
이럴때 바로 **접근제어가**자 나서야한다.

그럼 다음 접근제어자 편에서 김횡령을 어떻게 막는지 알아보자.
