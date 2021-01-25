# Types
- Primitive
- Object

## Primitive
```typescript
  // number
  const num:number = 2;

  // string
  const str:string = 'This is a string';

  // boolean
  const is_bool: boolean = false;

  // undefined
  let name: string | undefined;

  // null
  let person2: string | null;
  
  // unknown -> not recommended
  let notSure: unknown = 0;
  notSure = 'my';
  notSure = true;

  // any -> not recommended
  let anything: any = 0;
  anything = 'hello';

  // void
  function print():void
  {
      console.log('Hi');
      return;
  }

  // never -> never return
  function throwError(message: string): never
  {
      // message -> server (log)
      throw new Error(message);
      // Or
      // while(true)
      // {

      // }
  }

  // object
  let obj: object;
```

## Types with function
```typescript
  //JavaScript
  function jsAdd(num1, num2)
  {
      return num1 + num2;
  }

  //TypeScript
  function tsAdd(num1 : number, num2 : number) : number
  {
      return num1 + num2;
  }

  //JavaScript
  function jsFetchNum(id)
  {
      return new Promise((resolve, reject)=>
      {
          resolve(100);
      });
  }

  //TypeScript
  function tsFetchNum(id: string): Promise<number>
  {
      return new Promise((resolve, reject)=>
      {
          resolve(100);
      })
  }
```

## function parameter
```typescript
  // Optional parameter '?'
  function printName(firstName: string, lastName?: string)
  {
      console.log(firstName);
      console.log(lastName);
  }

  printName('Steve', 'Jobs');
  printName('Mini');
  printName('Anna');

  // Default parameter
  function printMessage(message: string = 'default message')
  {
      console.log(message);
  }
  printMessage();

  // Rest parameter
  function addNumbers(...numbers: number[]): number
  {
      return numbers.reduce((a, b) => a + b);
  }

  console.log(addNumbers(1, 2));
  console.log(addNumbers(1, 2, 3, 4));
```

## Array & Tuple
```typescript
  // Array : same types
  const fruits1: string[] = ['a', 'b'];
  const fruits2: Array<string> = ['a', 'b'];
  function printArray(fruits: readonly string[]){}  // readonly --> only for array[]


  // Tuple : different types -> not commonly used... replaced by : interface, type alias, class
  let student: [string, number];
  student = ['name', 123];
  student[0];                         // name
  student[1];                         // 123
  const[name, age] = student;
```

## Type Alises & String Literal Types
```typescript
  /**
   * Type Aliases
   */
  type Text = string;
  const name: Text = 'mini';
  const address: Text = 'Canada';

  type Num = number;

  type Student = 
  {
      name: string;
      age: number;
  };

  const student: Student = 
  {
      name: 'ellie',
      age: 12,
  };

  /**
   * String Literal Types
   */
  type Name = 'mini';
  let myName: Name;
  myName = 'mini';
  type JSON = 'json';
  const json: JSON = 'json';
```

## Union Types : OR
```typescript
  /**
   * Union Types: OR
   */

  type Direction = 'left' | 'right' | 'up' | 'down';

  function move(direction : Direction)
  {
      console.log(direction);
  }
  move('down');

  type TileSize = 8 | 16 | 32;
  const tile: TileSize = 16;

  // function: login -> success, fail
  type SuccessState = 
  {
      response:
      {
          body: string;
      };
  };

  type FailState = 
  {
      reason: string;
  }

  type LoginState = SuccessState | FailState;

  function login(): LoginState
  {
      return {
          response: 
          {
              body: 'logged in!',
          },
      };
  }

  // printLoginState(state: LoginState)
  // success -> body
  // fail -> reason
  function printLoginState(state: LoginState)
  {
      if('response' in state)
      {
          console.log(`${state.response.body}`);
      }
      else
      {
          console.log(`${state.reason}`);
      }
  }
```

## Discriminated Union : different types has same property
```typescript
  // function: login -> success, fail
  type SuccessState = 
  {
      result: 'success';
      response:
      {
          body: string;
      };
  };

  type FailState = 
  {   
      result: 'failed';
      reason: string;
  };

  type LoginState = SuccessState | FailState;

  function login(): LoginState
  {
      return {
          result: 'success',
          response: 
          {
              body: 'logged in!',
          },
      };
  }

  // printLoginState(state: LoginState)
  // success -> body
  // fail -> reason
  function printLoginState(state: LoginState)
  {
      if(state.result === 'success')
      {
          console.log(`${state.response.body}`);
      }
      else
      {
          console.log(`${state.reason}`);
      }
  }
```

## intersection type
```typescript
  /**
   * Intersection Types: &
   */
  type Student = 
  {
      name: string;
      score: number;
  };

  type Worker =
  {
      employeeId: number;
      work: () => void;
  }; 

  function interWork(person: Student & Worker)
  {
      console.log(person.name, person.score, person.employeeId, person.work());
  }

  interWork({
      name: 'mini',
      score: 10,
      employeeId: 1234,
      work: () => {},
  })
```

## enum
```typescript
 /**
 * Enum : not recommended in typescript -> Can be replaced by Union
 */
enum Days
{
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday,
}

console.log(Days.Tuesday);
const day = Days.Saturday;
console.log(day);
``

## Type Inference
```typescript
/**
 * Type Inference : not recommended
 */
let text = 'hello';
function print(message = 'hello')   // return automatically string
{
    console.log(message);
}
print('hello');

function add(x:number, y:number): number
{
    return x + y;
}
const result = add(1, 2);
```

## Type Assertion
```typescript
  /**
   * Type Assertion
   */
  function jsStrFunc(): any
  {
      return 2;
  }
  const result = jsStrFunc();
  console.log((result as string).length);
  console.log((<string>result).length);

  const wrong: any = 5;
  console.log((wrong as Array<number>).push(1));

  function findNumbers(): number[] | undefined
  {
      return undefined;
  }
  const numbers = findNumbers();
  numbers.push(2);

  const button = document.querySelector('class');
  if(button)
  {
      button.nodeValue;
  }
}
```
