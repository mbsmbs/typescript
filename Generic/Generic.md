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

# Comparison
```typescript
{
    interface Stack
    {
        readonly size: number;
        push(value: string): void;
        pop(): string;
    }

    type StackNode =
    {
        readonly value: string;
        readonly next?: StackNode;
    }

    class StackImpl implements Stack
    {
        private _size: number;
        private head?: StackNode;
        get size()
        {
            return this._size;
        }

        push(value: string)
        {
            const node: StackNode = {value: value, next: this.head};
            this.head = node; 
            this._size++;
        }

        pop(): string
        {
            if(this.head == null)
            {
                throw new Error('Stack is empty!');
            }
            const node = this.head;
            this.head = node.next;
            this._size--;

            return node.value;
        }
    }

    const stack = new StackImpl();
    stack.push('Min 1');
    stack.push('Steve 2');
    stack.push('Jobs 3');
    while(stack.size !== 0)
    {
        console.log(stack.pop());
    }
}
```
```typescript
{
    interface Stack<T>
    {
        readonly size: number;
        push(value: T): void;
        pop(): T;
    }

    type StackNode<T> =
    {
        readonly value: T;
        readonly next?: StackNode<T>;
    }

    class StackImpl<T> implements Stack<T>
    {
        private _size: number;
        private head?: StackNode<T>;

        constructor(private capacity: number){}

        get size()
        {
            return this._size;
        }

        push(value: T)
        {
            const node: StackNode<T> = {value, next: this.head};
            this.head = node; 
            this._size++;
        }

        pop(): T
        {
            if(this.head == null)
            {
                throw new Error('Stack is empty!');
            }
            const node = this.head;
            this.head = node.next;
            this._size--;

            return node.value;
        }
    }

    const stack = new StackImpl(10);
    stack.push('Min 1');
    stack.push('Steve 2');
    stack.push('Jobs 3');
    while(stack.size !== 0)
    {
        console.log(stack.pop());
    }
}
```
