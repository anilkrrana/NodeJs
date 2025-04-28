# NodeJs
Notes
challenge solution

const readline = require('readline');
const EventEmitter = require("events");
const { log } = require('console');
const emitter = new EventEmitter();

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

console.log(` 1. Login \n 2. Logout \n 3. Purchase \n 4. Profile Update \n 5. enter new choice \n 6. summry and exit`);
let summryData = {
    userLoggedIn: 0,
    userLogout: 0,
    purchase: 0,
    profileUpdate: 0
}

function ask(){
    rl.question('Enter your choice', (choice) => {
        if(choice === "1"){
            emitter.emit("userLogin", loginData, summryData);
            ask()
        }else if(choice === "2"){
            emitter.emit("userLogout", loginData, summryData);
            ask()
        }else if(choice === "3"){
            emitter.emit("purchase", "Laptop", summryData);
            ask()
        }else if(choice === "4"){
            emitter.emit("profileUpdate", loginData, summryData);
            ask()
        }else if(choice === "5"){
            ask();
        }else if(choice === "6"){
            emitter.emit("summry",summryData)
            console.log("exit");
            rl.close();
        }else{
            console.log("Incorrect choice, choose again");
            ask()
        }
    })
}
ask();


let loginData = {name: "Rohit"}


emitter.on("userLogin", (loginData, summryData) =>{
    console.log(`Hello ${loginData.name}, Your are successfully logged in`);
    summryData.userLoggedIn += 1
})

emitter.on("userLogout", (loginData, summryData) => {
    console.log(`Hello ${loginData.name}, Your are successfully logged out`);
    summryData.userLogout += 1
})

emitter.on('purchase', (product, summryData)=>{
    console.log(`Hello ${loginData.name}, You have successfully purchased ${product}`);
    summryData.purchase += 1
    
})

emitter.on('profileUpdate', (loginData, summryData)=>{
    console.log(`Hello ${loginData.name}, Your profile has been successfully updated`);
    summryData.profileUpdate += 1
    
})

emitter.on('summry', (summryData)=>{
    console.log(summryData);
    
})
