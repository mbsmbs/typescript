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
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }
    
    class CoffeeMaker
    {
        static BEANS_GRAMM_PER_SHOT: number = 7;
        coffeeBeans: number = 0;

        constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        makeCoffee(shots: number): CoffeeCup
        {
            if(this.coffeeBeans < shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }

            this.coffeeBeans -= shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT;
            return {
                shots: shots,
                hasMilk: false,
            }
        }
    }

    const maker: CoffeeMaker = new CoffeeMaker(21);
    maker.coffeeBeans += 3 * CoffeeMaker.BEANS_GRAMM_PER_SHOT;
    const coffee = maker.makeCoffee(3);
    console.log(coffee);
}
```

### 캡슐화 (encapsulation)
- public
- private
- protected
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }
    
    class CoffeeMaker
    {
        private static BEANS_GRAMM_PER_SHOT: number = 7;
        private coffeeBeans: number = 0;

        constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        static makeMachine(coffeeBeans: number): CoffeeMaker
        {
            return new CoffeeMaker(coffeeBeans);
        }

        fillCoffeeBeans(beans: number)
        {
            if(beans < 0)
            {
                throw new Error('Value for beans should be greater than 0');
            }
            this.coffeeBeans += beans;
        }

        makeCoffee(shots: number): CoffeeCup
        {
            if(this.coffeeBeans < shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }

            this.coffeeBeans -= shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT;
            return {
                shots: shots,
                hasMilk: false,
            }
        }
    }

    const maker: CoffeeMaker = new CoffeeMaker(32);
    maker.fillCoffeeBeans(21);
    console.log(maker);
}
```

### getter/setter
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }
    
    class CoffeeMaker
    {
        private static BEANS_GRAMM_PER_SHOT: number = 7;
        private coffeeBeans: number = 0;

        constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        static makeMachine(coffeeBeans: number): CoffeeMaker
        {
            return new CoffeeMaker(coffeeBeans);
        }

        fillCoffeeBeans(beans: number)
        {
            if(beans < 0)
            {
                throw new Error('Value for beans should be greater than 0');
            }
            this.coffeeBeans += beans;
        }

        makeCoffee(shots: number): CoffeeCup
        {
            if(this.coffeeBeans < shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }

            this.coffeeBeans -= shots * CoffeeMaker.BEANS_GRAMM_PER_SHOT;
            return {
                shots: shots,
                hasMilk: false,
            }
        }
    }

    const maker: CoffeeMaker = new CoffeeMaker(32);
    maker.fillCoffeeBeans(21);
    console.log(maker);

    class User
    {
        get fullName(): string
        {
            return `${this.firstName} ${this.lastName}`;
        }
        private internalAge = 4;
        get age(): number
        {
            return this.internalAge;
        }

        set age(num: number)
        {
            if(num < 0)
            {
                //...
            }
            this.internalAge = num;
        }

        constructor(private firstName: string, private lastName: string)
        {
        }
    }

    const user = new User('Steve', 'Jobs');
    user.age = 6;
    console.log(user.fullName);
}
```

### 추상화 Abstraction : 내부 복잡 외부 간편
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }

    interface CoffeeMaker
    {
        makeCoffee(shot:number): CoffeeCup;
    }
    
    class CoffeeMachine implements CoffeeMaker
    {
        private static BEANS_GRAMM_PER_SHOT: number = 7;
        private coffeeBeans: number = 0;

        private constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        static makeMachine(coffeeBeans: number): CoffeeMachine
        {
            return new CoffeeMachine(coffeeBeans);
        }

        fillCoffeeBeans(beans: number)
        {
            if(beans < 0)
            {
                throw new Error('Value for beans should be greater than 0');
            }
            this.coffeeBeans += beans;
        }

        private grindBeans(shots: number)
        {
            console.log(`grinding beans for ${shots}`);
            if(this.coffeeBeans < shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }
            this.coffeeBeans -= shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT; 
        }

        private preheat()
        {
            console.log('heating up...');
        }

        private extract(shots: number): CoffeeCup
        {
           console.log(`Pulling ${shots} shots...`);
           return {
                shots: shots,
                hasMilk: false,
            };  
        }

        makeCoffee(shots: number): CoffeeCup
        {
            this.grindBeans(shots);
            this.preheat();
            return this.extract(shots);
        }
    }

    const maker: CoffeeMachine = CoffeeMachine.makeMachine(32);
    maker.fillCoffeeBeans(32);
    maker.makeCoffee(2);
    console.log(maker);

    const maker2: CoffeeMaker = CoffeeMachine.makeMachine(32);
    maker2.makeCoffee(2);
    console.log(maker);
} 
```

### Interface
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }

    interface CoffeeMaker
    {
        makeCoffee(shots: number): CoffeeCup;
    }

    interface CommercialCoffeeMaker
    {
        makeCoffee(shots: number): CoffeeCup;
        fillCoffeeBeans(beans: number): void;
        clean(): void;
    }
    
    class CoffeeMachine implements CoffeeMaker, CommercialCoffeeMaker
    {
        private static BEANS_GRAMM_PER_SHOT: number = 7;
        private coffeeBeans: number = 0;

        private constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        static makeMachine(coffeeBeans: number): CoffeeMachine
        {
            return new CoffeeMachine(coffeeBeans);
        }

        fillCoffeeBeans(beans: number)
        {
            if(beans < 0)
            {
                throw new Error('Value for beans should be greater than 0');
            }
            this.coffeeBeans += beans;
        }

        clean()
        {
            console.log('Cleaning the machine...');
        }

        private grindBeans(shots: number)
        {
            console.log(`grinding beans for ${shots}`);
            if(this.coffeeBeans < shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }
            this.coffeeBeans -= shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT; 
        }

        private preheat()
        {
            console.log('heating up...');
        }

        private extract(shots: number): CoffeeCup
        {
           console.log(`Pulling ${shots} shots...`);
           return {
                shots: shots,
                hasMilk: false,
            };  
        }

        makeCoffee(shots: number): CoffeeCup
        {
            this.grindBeans(shots);
            this.preheat();
            return this.extract(shots);
        }
    }

    const maker: CoffeeMachine = CoffeeMachine.makeMachine(32);
    maker.fillCoffeeBeans(32);
    maker.makeCoffee(2);
    console.log(maker);

    const maker2: CommercialCoffeeMaker = CoffeeMachine.makeMachine(32);
    maker.fillCoffeeBeans(32);
    maker2.makeCoffee(2);
    maker2.clean();
    console.log(maker);

    class AmateurUser
    {
        constructor(private machine: CoffeeMaker){}
        makeCoffee()
        {
            const coffee = this.machine.makeCoffee(2);
            console.log(coffee);
        }
    }

    class ProBrarista
    {
        constructor(private machine: CommercialCoffeeMaker){}
        makeCoffee()
        {
            const coffee = this.machine.makeCoffee(2);
            console.log(coffee);
            this.machine.fillCoffeeBeans(45);
            this.machine.clean();
        }
    }

    const maker3: CoffeeMachine = CoffeeMachine.makeMachine(32);
    const amateur = new AmateurUser(maker);
    const pro = new ProBrarista(maker);
    amateur.makeCoffee();
    pro.makeCoffee();
} 
```

### Inheritance
```typescript
{
    type CoffeeCup = 
    {
        shots: number;
        hasMilk: boolean;
    }

    interface CoffeeMaker
    {
        makeCoffee(shots: number): CoffeeCup;
    }

    class CoffeeMachine implements CoffeeMaker
    {
        private static BEANS_GRAMM_PER_SHOT: number = 7;
        private coffeeBeans: number = 0;

        constructor(beans: number)
        {
            this.coffeeBeans = beans;
        }

        static makeMachine(coffeeBeans: number): CoffeeMachine
        {
            return new CoffeeMachine(coffeeBeans);
        }

        fillCoffeeBeans(beans: number)
        {
            if(beans < 0)
            {
                throw new Error('Value for beans should be greater than 0');
            }
            this.coffeeBeans += beans;
        }

        clean()
        {
            console.log('Cleaning the machine...');
        }

        private grindBeans(shots: number)
        {
            console.log(`grinding beans for ${shots}`);
            if(this.coffeeBeans < shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT)
            {
                throw new Error('Not enough coffee beans!');
            }
            this.coffeeBeans -= shots * CoffeeMachine.BEANS_GRAMM_PER_SHOT; 
        }

        private preheat()
        {
            console.log('heating up...');
        }

        private extract(shots: number): CoffeeCup
        {
           console.log(`Pulling ${shots} shots...`);
           return {
                shots: shots,
                hasMilk: false,
            };  
        }

        makeCoffee(shots: number): CoffeeCup
        {
            this.grindBeans(shots);
            this.preheat();
            return this.extract(shots);
        }
    }

    class CaffeLatteMachine extends CoffeeMachine
    {
        constructor(beans: number, public readonly serialNumber: string)
        {
            super(beans);
        }

        private steamMilk()
        {
            console.log('SteamMing some milk...');
            
        }

       makeCoffee(shots: number): CoffeeCup
       {
           const coffee = super.makeCoffee(shots);
           this.steamMilk();
           return{
               ...coffee,
               hasMilk: true,
           }
       }
    }

    const machine = new CoffeeMachine(23);
    const latteMachine = new CaffeLatteMachine(23, 'abcd');
    const coffee = latteMachine.makeCoffee(1);
    console.log(coffee);
    console.log(latteMachine.serialNumber);
    
} 
```

### Polymorphism
