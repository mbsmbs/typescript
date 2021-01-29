# OOP

## 4 Principles
1. Encapsulation
- 연관된 데이터 밑 메서드들을 묶고 외부에 공개할지 말지 결정하는 것
2. Abstraction
- 안에 어떻게 구현되었는지는 몰라도 지정된 인터페이스 함수를 통해 object를 사용하는 것
3. Inheritance
- 이미 존재하는 클래스의 데이터와 메서드들을 가져다 새로운 클래스에서 쓸 수 있다.
4. Polymorphism
- 같은 이름의 동작이지만 다르게 동작하는 것


## 커피기계 만들기

### 절차지향적
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }

    const BEANS_GRAMM_PER_SHOT: number = 7;

    let coffeeBeans: number = 0;

    function makeCoffee(shots: number): CoffeeCup
    {
        if(coffeeBeans < shots * BEANS_GRAMM_PER_SHOT)
        {
            throw new Error('Not enough coffee beans!');
        }

        coffeeBeans -= shots * BEANS_GRAMM_PER_SHOT;
        return {
            shots: shots,
            hasMilk: false,
        }
    }

    coffeeBeans += 3 * BEANS_GRAMM_PER_SHOT;
    const coffee = makeCoffee(2);
    console.log(coffee);
}
```

### OOP
