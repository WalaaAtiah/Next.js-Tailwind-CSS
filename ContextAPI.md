# Context API lab 34[source](https://reactjs.org/docs/context.html)

**Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree.**

## example for use context API
1. authontication 
2. languges
3. location
4. theam (dark,light)
5. setting 

## compare between use props and context API

### * PROPS :Dynamic ,pass data between components 
### * context API :almost static data ,each components can pass data directly from the context file 

# theme context 

## Toggling dark mode manually[source](https://tailwindcss.com/docs/dark-mode)
1. in the element `className="dark:bd-black"` 
2. in the `body` inside the `layout.js` add `class="dark"` //add this class for the perant of the components
3. in the `tailwind.config.js`
```
module.exports = {
  darkMode: 'class',
  // ...
}
```

## How create the context API 

## `APP ---Context ---- theme.js`
### 1. Create provider that will provide the globale state to my app  
### 2. create the context 
### 3.create the context Wrapper(provider )

```
import { createContext, useEffect, useState } from "react"
// 1.1 create the context
export const ThemeContext = createContext();

// 1.2 create the context wrapper (provider)
export default function ThemeWrapper({children}){

    const [isDarkTheme, setIsDarkTheme] = useState(true);

    function initialThemeHandle(){
        // take the initial value
        isDarkTheme && document.querySelector("body").classList.add("dark"); // add dark class to the body element
    }
    
    function toggleThemeHandler() {
        setIsDarkTheme(!isDarkTheme);
        document.querySelector("body").classList.toggle("dark"); // add dark class to the body element
    }
    
    const globalState = {
        isDarkTheme: true,
        toggleThemeHandler
    }

    useEffect(()=>initialThemeHandle());

    return(
        <ThemeContext.Provider value={globalState}>
            {children}
        </ThemeContext.Provider>
    )

}

```

## `layout.jsx`
```
<ThemeWrapper>

      <body>
        <Header />
        <main>
          {children}
        </main>
        <Footer />
      </body>
      </ThemeWrapper>
```

## `header.js` : add the button that chang the Theme 

```
import { useContext } from 'react';
import {ThemeContext} from '../contexts/theme'
export default function Header(){

    const {isDarkTheme, toggleThemeHandler} = useContext(ThemeContext);
    console.log(useContext(ThemeContext));

    return(
        <header>
            <nav className='flex flex-wrap items-center px-3 bg-cyan-900 dark:bg-slate-900'>
                        <button
                            type="button"
                            className="py-1 sm:py-2.5 px-2 sm:px-5 mr-2 bg-zinc-300 text-black dark:bg-slate-800 dark:text-white rounded"
                            onClick={toggleThemeHandler}
                        >Toggel Theme</button>
                    
            </nav>
        </header>
    )
}
```