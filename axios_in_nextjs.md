# axios 
1. get user aouthentication and access token 

```
async function login(userInfo) {
        // end a request to the server 
        console.log(1,userInfo)
        const url = "https://cookie-w-a.herokuapp.com/api/token/"; // the server url
        try{

            const res = await axios.post(url, userInfo);
            console.log(2,res.data)
            SetGlobalState({
                tokens : res.data,
                login,
            })
        }catch {
            console.log("error")
        }

    }
```

2. post 

* access token 
```
const { tokens } = useContext(AuthContext);
    const config = {
        headers: {
            'Authorization': `Bearer ${tokens.access}`
        }
    }
```
* do the post methof inside function 

```
const userData = {
            location: location,
            "description": "test2",
            "hourly_sales": {
                "test2": "test"
            },
            minimum_customers_per_hour: Minimum,
            maximum_customers_per_hour: Maximum,
            average_cookies_per_sale: Average,
            "owner": 2
        };
        
    

        console.log(userData);
        const url = "https://cookie-w-a.herokuapp.com/api/v1/cookie_stands/"; // the server url
        console.log(url)

        axios.post(url, userData, config).then(res =>res.data).catch(function(error){
            console.log(error);
        });
```

3. get by use SWR

1. INSTALL `npm install swr`
2. import it `import useSWR from 'swr'`
3. add this 

```
const config = {
        headers: {
            'Authorization': `Bearer ${tokens.access}`
        }
    }
    const url = "https://cookie-w-a.herokuapp.com/api/v1/cookie_stands/"; // the server url
    
    const fetcher = url => axios.get(url, config).then(res => res.data);
    // console.log("fetcher",fetcher)

    const { data, error, isLoading } = useSWR(url, fetcher);
    
    console.log(data);
    
    if (error) return <div>failed to load</div>
    if (isLoading) return <div>loading...</div>
```


4. delete 

``` 
const deleteHandeler=(id)=>{
        console.log('deleteHandeler',id,url+id.toString())
        axios.delete(url+id.toString(), config).then(res =>res.data).catch(function(error){
            console.log(error);
        });
        
    }
```