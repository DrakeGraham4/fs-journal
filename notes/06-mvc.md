# MVC

View (DOM)- has button onclick= "feedAnimal()

Controller (js) -- controller passes the input of the button feedanimal() the controller takes information from the View and also passes info from the view. Controller holds the function

Service (business logic)-

Model (data structure/blueprint)-

Proxystate (appstate)

constructor is very unique method for the class

bcw create --> mvc----> project name---> hit enter, code .

make animal.js under models
export class Animal{
constructor(name, type, age, carnivore, flight){
console.log('creating an animal')
this.name = name
this.type = type
this.age = age
this.eatsMeat = carnivore
this.flight = flight

    }
    hello(){
        console.log(`${this.name}, the ${this.canFly ? 'flying' : '')
    }

}

go to service

go to orange symbol on animal and hit tab to import from animal.js

let animal1 = new Animal('koko', 'Gorilla', 43, true, false)
let animal2 = new Animal('Tim', 'Turtle', 200, true, true)
let animal3 = ('Sebastian', 'Sloth', 5, true, false)

let allAnimals = [animal1, animal2, animal3]

-------Tuesday 2/15/2022-------

bcw serve, hit plus, npm run sass to use main.css

1. Start by creating all files, controllers, models, service

2. Start with controller. export class "Game"Controller{

}

3. Go to "Game"Service. Make class "Game"Service{

}
then make export const with lowercase "game"Service = new Uppercase "Game"Service()

4. Go to Model.js/"Monster".js.

5. Come back to AppState within the event emitter add activeMonster = new Monster()
