# Custom Hook lab33 [source](https://reactjs.org/docs/hooks-custom.html)

## When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

<br>

## A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks. For example, useFriendStatus below is our first custom Hook:

1. 
```
export function useMostRepeated(pets, searchedArr){
    
    //write the function that you want
}
export default useMostRepeated 
```
2. Now that we’ve extracted this logic to a useFriendStatus hook, we can just use it:

```
import {useMostRepeated} from '../custom_hooks/useMostRepeated.js';
const isOnline = useFriendStatus(props.friend.id);
```

