we laearm react :
step1:install pakages:-  npx create-react-app folder_Name

step2: goto Html files inside the public folder
then remove all link part or comments

step 3:goto src folder remove all files except app.js or index.js

step 4:which files are deleted then you are also deleted imported roots

topic :::

/*   
# 1.Components:
  components are independent and reusable bits of code. they serve the same pupose as javascripts function,but work in isolation and return HTML.

syntax:

funtion Compoents()=>{
    return (
        <div> Components<div/>
    )
}
export default Components



# 2.JSX:
JSX allows us to write HTML in react. JSX makes it easier to write and add HTMl in react 
























































# 1.Project  ::Counter

# counter.js

import { useState } from "react";

import "./style.css"

function Counter() {
const [count,setCount]=useState(0);

const increment=()=>{
    setCount(count+1)
}

const decrement=()=>{
    setCount(count-1)
}

  return (
    <>
  <div className="container">
    <h1 className="number">{count}</h1>
  </div>
   <section className="btns-container">
    <button onClick={increment} className="increment">+</button>
    <button onClick={decrement} className="decrement">- </button>
   </section>
   </>
  )
}

export default Counter;


# style.css


*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
} 
body{
    background-color: rgb(4, 4, 4);
    height: 100vh;
    display: flex;
    flex-direction:column;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: aliceblue;
}

.container.number{
    font-size: 6rem;
}

.btns-container{
    width: 40rem;
    display: flex;
    justify-content: space-around;
    margin: 5rem;
}

.increment{
    padding: 10px 20px;
    border-radius: 100px;
    font-size: 2rem;
    background: #141517;
    color: #fff;
    cursor: pointer;
}

.decrement{
    padding: 10px 25px;
    border-radius: 100%;
    font-size: 2rem;
    background: #141517;
    color: #fff;
    cursor: pointer;
}


# 2. Project: ::Todo

Todo.js
import { useState } from "react";
import "./style.css";



function generteId(){
  return Math.floor(Math.random()*100)
}
function Todo(){

const [todos,setTodos]=useState([]);
const [input,setInput]=useState("");


  const handleSubmit=()=>{
    setTodos(todos=>
      todos.concat({
        text:input,
        id:generteId()
      })
    );
      setInput('')
    };
  

  const removeTodo=(id)=>{
    setTodos((todos)=>todos.filter((t)=>t.id!==id));
  }
  return (
  <>
  <div className="container">
    <input type="text" value={input} onChange={(e)=>setInput(e.target.value)} placeholder="New Todo" />
    <button onClick={handleSubmit}>Submit</button>

<ul className="todos-list">
  
    {todos.map(({text,id})=>{
    return  <li key={id} className="todo">
<span>{text}</span>
<button className="close" onClick={()=>removeTodo(id)}>X</button>

      </li>
    })
  }
</ul>

  </div>
  </>
  )
}

export default Todo;

# style.css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
} 

body{
      display: flex;
      justify-content: center;
      align-items: center;
}
.container{
    background: #fff;
    padding: 50px;

}
input{
    padding: 15px;
    border: none;
    outline: none;
    background: #f5f9eb;
    width: 300px;
    margin-right: 10px;
}
    button{
        border-radius: 100px;
        background: #454545;
        padding: 5px;
        border: none;
        outline: none;
        color: #fff;
        padding: 10px 20px;
        cursor: pointer
        ;
    }


    .todos-list{
        margin-top: 3rem;

    }
    
    .todo{
         list-style: none;
         display: flex;
         justify-content: space-between;
         align-items: center;
         background: #f5f5f9eb ;
         padding: 7px 20px;
         margin: 10px;
         font-family: sans-serif;
    }

    .close{
        padding: 5px,10px;
        cursor:  ;
    }



# 3. Project::Meals API Project

# main.js

import axios from "axios"
import {useEffect, useState } from "react";
import "./style.css";

function Main(){
const [items,setItems]=useState([]);

useEffect(()=>{
  axios
  .get("https://www.themealdb.com/api/json/v1/1/filter.php?c=Seafood")

  .then((res)=>{
    console.log(res.data);
    setItems(res.data.meals);
  })
  .catch((err)=>{
    console.log(err );
  })
},[]);

const itemslist=items.map(({strMeal,strMealThumb,idMeal})=>{
  return(
    <section className="card">
      <img src={strMealThumb} />

      <section className="content">
        <p>{strMeal}</p>
        <p>#{idMeal}</p>
      </section>
    </section>   
  );
})
  return <div className="items-container">{itemslist}</div>
}

export default Main;


# style.css
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  
  .items-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 10px;
  }
  
  .card {
    background: rgb(255, 249, 249);
    font-size: 12px;
    color: rgb(68, 68, 68);
    margin: 10px;
    padding: 30px;
    transition: 1s ease;
    cursor: pointer;
  }
  
  .card:hover {
    transform: scale(1.1);
  }
  
  .content {
    display: flex;
    justify-content: space-between;
    font-family: sans-serif;
    margin-top: 20px;
  }
  
  p {
    font-weight: bold;
  }
  
  img {
    border-radius: 5px;
    height: 200px;
    width: 300px;
  }
  

  # 4.project: Calculator
# Main.js
import { useState } from "react";
import "./style.css";

function Main() {
  const [inputvalue, setinputvalue] = useState("");

  function display(value) {
    setinputvalue(inputvalue + value);
  }

  function calculate() {
    var answers = eval(inputvalue);
    setinputvalue(answers);
  }

  function clear() {
    setinputvalue("");
  }

  return (
    <form class="calculator" name="calc">
      <input type="text" class="value" value={inputvalue} />
      <span class="num clear" onClick={() => clear()}>
        c
      </span>
      <span onClick={() => display("/")}>/</span>
      <span onClick={() => display("*")}>*</span>
      <span onClick={() => display("7")}>7</span>
      <span onClick={() => display("8")}>8</span>
      <span onClick={() => display("9")}>9</span>
      <span onClick={() => display("-")}>-</span>
      <span onClick={() => display("4")}>4</span>
      <span onClick={() => display("5")}>5</span>
      <span onClick={() => display("6")}>6</span>
      <span className="plus" onClick={() => display("+")}>
        +
      </span>
      <span onClick={() => display("1")}>1</span>
      <span onClick={() => display("2")}>2</span>
      <span onClick={() => display("3")}>3</span>
      <span onClick={() => display("0")}>0</span>
      <span onClick={() => display("00")}>00</span>
      <span onClick={() => display(".")}>.</span>
      <span class="num equal" onClick={() => calculate()}>
        =
      </span>
    </form>
  );
}

export default Main;


 # style.css:
 * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #1b1b1b;
}

.calculator {
  position: relative;
  display: grid;
}

.calculator .value {
  grid-column: span 4;
  height: 100px;
  text-align: right;
  border: none;
  outline: none;
  padding: 10px;
  font-size: 18px;
}

.calculator span {
  display: grid;
  width: 60px;
  height: 60px;
  background: #292929;
  place-items: center;
  border: 1px solid rgba(114, 110, 110, 0.1);
  color: #0ae927;
}

.calculator span:active {
  background: rgb(145, 142, 123);
  color: #fff;
}

.calculator span.clear {
  grid-column: span 2;
  width: 120px;
  background: rgba(183, 190, 80, 0.27);
  /* color: #fff; */
}

.calculator span.plus {
  grid-row: span 2;
  height: 120px;
}

.calculator span.equal {
  background: rgb(255, 163, 26);
  /* background: #03b1ff; */
}

# 5. project ::Color Toggler
# ToogleButtopnColor:
import React, { useState } from "react";
import "./style.css"
function ToggleBackgroundColor() {
  const [backgroundColor, setBackgroundColor] = useState("white");
  const [textColor, setTextColor] = useState("#1b1b1b");
  const [buttonStyle, setButtonStyle] = useState("white");

  function handleClick() {
    setBackgroundColor(backgroundColor === "white" ? "#1b1b1b" : "white");
    setTextColor(textColor === "#1b1b1b" ? "#ffa31a" : "#1b1b1b");
    setButtonStyle(backgroundColor === "white" ? "#1b1b1b" : "white");
  }

  return (
    <section style={{ backgroundColor, color: textColor }}>
      <button
        onClick={handleClick}
        style={{
          buttonStyle,
          color: textColor,
          border: `2px solid ${textColor}`,
        }}
      >
        {backgroundColor === "#1b1b1b" ? "Black Theme" : "White Theme"}
      </button>
      <section className="content">
        <h1>
          Welcome To A <br /> Real World..
        </h1>
      </section>
    </section>
  );
}

export default ToggleBackgroundColor;


# 6. Project: serch Icon Project

# HiddenSearchBar.js

import React, { useState } from "react";
import { FaSearch } from "react-icons/fa";
import "./style.css"
function HiddenSearchBar() {
  const[showInput,setShowInput]=useState(false);
  const[BgColor,setBgColor]=useState("white");

  const handleClick=(e)=>{
    setBgColor("#1a1a1a")
    if(e.target.className==="container"){
      setShowInput(false)
      setBgColor("#fff")
    }
  }
  return (
  <>
<section 
className="container"
style={{backgroundColor:BgColor}}
onClick={handleClick}
>
{showInput ? (
  <input type="text" placeholder="Search..." />
):(
  < FaSearch onClick={ () => setShowInput(true)} />
)}
</section>

  </>
  )

}

export default HiddenSearchBar;


# style.css


* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
 
section{
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transform: 0.7s ease;
}

input{
   padding: 13px 12px;
   background: transparent;
   outline: none;
   border: 1px solid #fff;
   color: #fff;
   border-radius: 2px;
   box-sizing: 2px 2px 1px;
   box-shadow: rgb(35,35,35);

}


# 7.project

# Testimonials:
import React, { useState } from "react";
import "./style.css"
function Testimonials() {

  const [currentIndex,setCurrentIndex]=useState(0);

  const testimonials=[{
    quote:"This is the best product I've ever used!",
    author:"Kundan Thakur"
  },
{
   quote:"I Highly rcomendation this product to everyone",
    author:"Abhishek Kumar"
},
{
   quote:"This product has completely changed my Life",
    author:"Lallu LAl"
}
];

const handlePrevClick=()=>{
  setCurrentIndex(
    (currentIndex+testimonials.length-1)%testimonials.length
  )
}


const handleNextClick=()=>{
  setCurrentIndex(
    (currentIndex+1)%testimonials.length
  )
}
  return (
  <>

  <div className="testimonials">

<div className="testimonials-quote">
  {
    testimonials[currentIndex].quote
   }

</div>
<div className="testimonials-author">
   {
    testimonials[currentIndex].author
   }
  </div>

<testimonials className="testimonials-nav">

<button onClick={handlePrevClick}>Prev</button>
<button onClick={handleNextClick} >Next</button>
</testimonials>

  </div>
  </>
  )

}

export default Testimonials;


# style.css

@import url('https://fonts.googleapis.com/css2?family=Balthazar&family=Bungee+Tint&family=Italianno&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Balthazar&family=Bruno+Ace+SC&family=Bungee+Tint&family=Italianno&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
 
body{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #e8faff;
}
.testimonials{
  margin: 0 auto;
  text-align: center;
  font-family: sans-serif;
  border-radius: 10px;
  padding: 40px;
  box-shadow: 0 0 10px rgb(0,0,0,0.1);

}
.testimonials-quote{
  font-size: 22px;
  font-family: "Balthazar", serif;
  margin-bottom: 10px;
  color: #666;
}

.testimonials-author{
  font-size: 18px;
  font-family: "Bruno Ace SC", sans-serif;
  margin-bottom: 20px;
  color: #050404;
}


.testimonials-nav{
  display: flex;
  justify-content: space-around;

}

.testimonials-nav button{
  padding: 2px 4px;
  border: none;
  background: #05bcf3;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;

}



# 8.project ::

# Accordion.js::
import React, { useState } from "react";
import "./style.css"

function Accordion({title,content}) {

  const[isActive,setIsActive]=useState(false);

  return <section className="acccordion-card">
    <div className="header" onClick={()=>setIsActive(!isActive)}>
      <div>{title}</div>
      <p className="icon"> {isActive?"-":"+"}</p>
    </div>
    <div className="content">{isActive&&<p className="card-info">{content}</p>}</div>
  </section>

}

export default Accordion;

# style.css ::


* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

body{
  background: rgb(36, 36, 36);
  color: #fff;
  font-family: sans-serif;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.acccordion-card{
  margin: 20px;
  padding: 20px;
  background: rgb(73, 73, 73);

} 

.header{
  display: flex;
  justify-content:space-between;
  width: 40rem;

}
 
.icon{
  font-size: 1.5rem;
  cursor: pointer;
} 
p.card-info{
  width: 30rem;
  padding: 20px 10;
  line-height: 1.3;

}

#  C:\Users\kundan\Desktop\myapp\src\utils

# content.js
export const accordionData = [
  {
    title: "What Is HTML?",
    content: `The HyperText Markup Language or HTML is the standard markup language for documents designed to be displayed in a web browser. It can be assisted by technologies such as Cascading Style Sheets and scripting languages such as JavaScript.`,
  },
  {
    title: "What Is React?",
    content: `React is a free and open-source front-end JavaScript library for building user interfaces based on UI components. It is maintained by Meta and a community of individual developers and companies.`,
  },
  {
    title: "What Is Node.js?",
    content: `Node.js is a cross-platform, open-source server environment that can run on Windows, Linux, Unix, macOS, and more. Node.js is a back-end JavaScript runtime environment, runs on the V8 JavaScript Engine, and executes JavaScript code outside a web browser.`,
  },
  {
    title: "What Is Golang?",
    content: `Go is a statically typed, compiled programming language designed at Google by Robert Griesemer, Rob Pike, and Ken Thompson. It is syntactically similar to C, but with memory safety, garbage collection, structural typing, and CSP-style concurrency`,
  },
];


# App.js ::

import Accordion from "./Accordion.js";
import {accordionData} from "./utils/content.js";

const App=()=> {
  return (
    <div>
      <div className="Accordion">
        {accordionData.map(({ title, content }, index) => (
          <Accordion key={index} title={title} content={content} />
        ))}
      </div>
    </div>
  );
};

export default App;





               */