# MEMOIZATION  lab 33:[source1](https://www.freecodecamp.org/news/memoization-in-javascript-and-react/),[source2](https://www.topcoder.com/thrive/articles/memoization-in-react-js)


##  1. MEMOIZATION USING MEMO :
in this example render the greeting  function just when the user change the name , and when chang the addres doesn't render 

```
import { memo, useState } from "react";

export default function MyApp() {
    const [name, setName] = useState('');
    const [address, setAddress] = useState('');

    return (
        <>
            <label>
                Name{': '}
                <input value={name} onChange={e => setName(e.target.value)} />
            </label>
            <label>
                Address{': '}
                <input value={address} onChange={e => setAddress(e.target.value)} />
            </label>

            <Greetings name={name}/>
        </>
    )
}
# create another component in the same file 
const Greetings = memo(function Greetings({name}) {
    console.log("Greeting is re-rendered")
    return(<h3>{name}</h3>)
})
```


## 2. MEMOIZATION USING USEMEMO

**it is like remember the value invariable and when this variable change do the function**
   
```
import {useMemo} from 'react';
let petImages = useMemo(()=>{
        return filterPets(pets, mostRepeatedPet)
    }, [mostRepeatedPet])


```
