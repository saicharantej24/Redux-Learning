# Redux
```text
---Creating a themecontext to share data w/o passing it through every component.
---Think of it like a global bulletin board where you can post data and any component can read it.
```
# context/ThemeContext.js :
```js
import {createContext} from "react";
const ThemeContext=createContext();
export default ThemeContext;
```
```text
App.js:This is the root component that wraps everything with the Context Provider:
a-->Provider = the one who posts on the bulletin board
b-->value="white" = the data being shared (the theme is "white")
c-->Everything inside can access this "white" value
```
# App.js
```js
import ThemeContext from "./context/ThemeContext";
import ChangeThemeBtn from "./components/ChangeThemeBtn";
function App() {
  return (
    <div className="App">
      <ThemeContext.Provider value="white">
        <ChangeThemeBtn/>
      </ThemeContext.Provider>
    </div>
  );
}    

export default App;
```
```text
useContext = reads the bulletin board
Shows a button and renders the Test component inside it
```
# components/ChangeThemeBtn.jsx :
```js
import React,{useContext} from "react";
import ThemeContext from "../context/ThemeContext";
import Test from "./Test";
const ChangeThemeBtn=()=>{
    // This component reads the theme data:
    const data=useContext(ThemeContext);
    return (
        <div>
        <button>Change Theme</button>
        <Test/>
        </div>
        
    );
};
export default ChangeThemeBtn;
```
# components/Test.jsx:
```js
import React,{useContext} from "react";
import ThemeContext from "../context/ThemeContext";
// It also has access to the same theme value
const Test=()=>
{
    const data=useContext(ThemeContext);
    return (
        <div>
            <h1>Test</h1>
        </div>
    )

}
export default Test;
```
--------------------------***************----------------------------------
```text
wrapping everything in App.js is not good Idea
```
# ThemeContext.js:
```js
import {createContext} from "react";
const ThemeContext=createContext();
export const ThemeContextProvider=({children})=>
{
    return(
        <ThemeContext.Provider value={"white"}>{children}
        </ThemeContext.Provider>
    );
};
export default ThemeContext;
```
# App.js
```js
import {ThemeContextProvider} from "./context/ThemeContext";
import ChangeThemeBtn from "./components/ChangeThemeBtn";
function App() {
  return (
    <div className="App">
      <ThemeContextProvider >
        <ChangeThemeBtn/>
      </ThemeContextProvider>
    </div>
  );
}    

export default App;
```




