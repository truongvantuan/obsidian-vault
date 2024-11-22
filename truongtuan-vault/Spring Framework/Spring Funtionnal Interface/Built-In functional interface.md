## Customizer
Accepts a single input and return no result.
- Performs the customizations on the input argument.
```
void customize(T t);
```
- Does not alter the input argument
```
static <T> Customizer<T> withDefaults() {  
    return (t) -> {  
    };  
}
```
## 
