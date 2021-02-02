# Generic Function
```typescript
{
    function checkNotNull<T>(arg: T | null): T
    {
        if(arg == null)
        {
            throw new Error('not valid number!');
        }
        return arg;
    }
    const number = checkNotNull(123);
    const boal: boolean = checkNotNull(true); 

}
```


# Generic Class
```typescript
{
    interface Either<L, R>
    {
        left: () => L;
        right: () => R;
    }
    
    class SimpleEither<L, R> implements Either<L, R>
    {
        constructor(private leftValue: L, private rightValue: R){}

        left(): L
        {
            return this.leftValue;
        }

        right(): R
        {
            return this.rightValue;
        }
    }

    const either: Either<number, number> = new SimpleEither(4, 5);
    either.left();
    either.right();

    const best = new SimpleEither({name: 'Ellie'}, 'hello');
}
```

# Constraints
```typescript
{
    interface Employee
    {
        pay(): void;
    }

    class FullTimeEmployee implements Employee
    {
        pay()
        {
            console.log('Full Time!');
        }

        workFullTime()
        {

        }
    }

    class PartTimeEmployee implements Employee
    {
        pay()
        {
            console.log('Part Time!');
        }

        workPartTime()
        {
            
        }
    }

    function payBad(employee: Employee): Employee
    {
        employee.pay();
        return employee;
    }

    function payGood<T extends Employee>(employee: T): T
    {
        employee.pay();
        return employee;
    }

    const steve = new FullTimeEmployee();
    const jobs = new PartTimeEmployee();
    steve.workFullTime();
    jobs.workPartTime();

    const steveAfterPay = payGood(steve);
    const jobsAfterPay = payGood(jobs);

    // ---------
    const obj = 
    {
        name: 'steve',
        age: 20, 
    };

    const obj2 =
    {
        animal: 'dog',
    }

    console.log(getValue(obj, 'name'));
    console.log(getValue(obj, 'age'));
    console.log(getValue(obj2, 'animal'));

    function getValue<T, K extends keyof T>(obj: T, key: K): T[K]
    {
        return obj[key];
    }
    
}
```
