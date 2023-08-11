# CapitalOne24HourProject

//write your code here
import promptSync from 'prompt-sync';
import chalk from "chalk";
import inquirer from "inquirer";
import chalkAnimation from "chalk-animation";
import figlet from "figlet";
import gradient from 'gradient-string'
import { createSpinner } from "nanospinner";

// Daniella Lacotera | Capital One Tech Mini Mester Project | Cohort 2 // Aug. 8 , 2023
// Description: User is given the task to guess the computer's guess



//Global variables
 let prompt = promptSync();
 let playerName;
 let userNum;
 const spinner = createSpinner("Checking guess...");
 const resolveAnimations = (ms = 3000) => new Promise((resolve) => setTimeout(resolve, ms));


//Main function that starts the functions for the game
main();

// given function to present and display animations for each function
async function main(){
  await guessGame();
  await winner(playerName,userNum);

}

async function guessGame(){
  //Random number generated
var num = Math.floor(Math.random() *100);

//Introduction to game
console.log("Computer Number ",num);
console.log(gradient.pastel.multiline("______________________________________________________________________________________________________\n"));
console.log(gradient.pastel.multiline("Welcome to guessing the number game!"));
playerName = prompt(gradient.pastel.multiline("What is your name player? "));
console.log(gradient.pastel.multiline("You have to guess a number from 1-100," + playerName));   
 

//Loop to check the value of the user's number compared to the computer's number
while(userNum != num) {
userNum = prompt(gradient.pastel.multiline("Type a number to start guessing!           "));
console.log(gradient.pastel.multiline("Your number is :  _"), chalk.underline.bgGrey(userNum), "_");
      spinner.start();
      await resolveAnimations(); 
    
  if  ( userNum > 100 || userNum <= 0 )
    {   
      spinner.error({text: `${chalk.red('That number is not in the range! Please choose in the range!')}`});
    }
    else if( userNum < num) 
    {
        spinner.error({text: `${chalk.red('Low!')}`});
    }
    else if (userNum > num) 
    {
      spinner.error({text: `${chalk.red('High!')}`});
    }
    else
    {
      spinner.success({text: `${chalk.greenBright('You guessed it!\n')}`});
    }
  }
}


//Displays win screen to winner
 async function winner(playerName,userNum) {  
    figlet(`Congratulations , ${playerName} !`, (err, data) => {
      console.log(gradient.pastel.multiline(data) + '\n');
      console.log(gradient.pastel.multiline("The number you had to guess was " + userNum +" !!!!!!") + '\n');  
      console.log(chalk.italic(`Thank you Capital One for allowing me to participate in Capital One's Tech Mini Mester!`));
      console.log(chalk.italic(`We Do the Right Thing through five principles: Open; Teamwork; Respect for Each Other; Respect for Our Customers; and Integrity.`))
      console.log(gradient.pastel.multiline("______________________________________________________________________________________________________\n"));
      process.exit(0); 


    }
  );
}








