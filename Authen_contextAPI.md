# Authentication contextAPI

1. create this file `app.js---- context----Auth.js` 
2. npm i axios
3. `Auth.js`

```
import { createContext, useState } from "react"
import axios from "axios";

// 1.1 create the context
export const AuthContext = createContext();

// 1.2 create the context wrapper (provider)
export default function AuthWrapper({children}){

    const [globalState, SetGlobalState] = useState({
        tokens : null,
        login,
    })

    async function login(userInfo) {
        // userInfo={username :"",passward:""}
        // end a request to the server 
        const url = "http://localhost:8000/api/token/"; // the server url
        const res = await axios.post(url, userInfo);
        // console.log(res.data)
        SetGlobalState({
            tokens : res.data,
            login,
        })
    }

    return(
        <AuthContext.Provider value=''>
            {children}
        </AuthContext.Provider>
    )

}

```
4. create New componenet `Loginform.js` :

```
import Image from 'next/image';
import { useState,useContext } from 'react';
import { AuthContext } from '../Context/Auth';

export default function LoginForm() {
    const [username,SetUsername]= useState("");
    const [password,SetPassword]= useState("");
    const {login} = useContext(AuthContext);

    const UsernameHandeler=(e)=>{
        SetUsername(e.target.value);
    }
    const PasswordHandeler=(e)=>{
        SetPassword(e.target.value);
    }

    const ClickHandeler=(e)=>{
        
        console.log(username,password);
        login({username,password})

    }

    return (


        <div class="w-full h-screen flex">
            <Image
                src="https://images.unsplash.com/photo-1540569876033-6e5d046a1d77?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80"
                alt="background"
                width={500}
                height={100}
                class="object-cover object-center h-screen w-7/12">

            </Image>
            <div class="bg-white flex flex-col justify-center items-center w-5/12 shadow-lg">
                <h1 class="text-3xl font-bold text-orange-500 mb-2">LOGIN</h1>
                <div class="w-1/2 text-center">
                    <input type="text" name="username" placeholder="username" autocomplete="off" onChange={UsernameHandeler}
                        class="shadow-md border w-full h-10 px-3 py-2 text-orange-500 focus:outline-none focus:border-orange-500 mb-3 rounded" />
                    <input onChange={PasswordHandeler} type="password" name="password" placeholder="password" autocomplete="off"
                        class="shadow-md border w-full h-10 px-3 py-2 text-orange-500 focus:outline-none focus:border-orange-500 mb-3 rounded" />
                    <button onClick={ClickHandeler}  class="bg-orange-500 hover:bg-orange-600 text-white px-3 py-1 rounded text-lg focus:outline-none shadow">Sign In</button>

                </div>
            </div>
           
        </div>





    )
}
```
5. in the `layout.js`

```
 <AuthWrapper>

      <body className='dark:bg-[#0c3135] 	 '>
        <Header />
        <main className='dark:bg-[#0c3135]'>
          {children}
        </main>
        <Footer />
      </body>
        </AuthWrapper>
  
```