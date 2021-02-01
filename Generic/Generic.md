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


# Generic class
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
