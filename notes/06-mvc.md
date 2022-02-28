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

-------Monday 2/21/2022 External API's------

1. API- application programming interface

2. Go to fetch/hxr in Network tab to see where the info that your page requested from your api. look at preview and you can see the info. Have tab open or it won't

3. CRUD method- Create, Read, Update, Delete/Destroy

4. http.cat for determining error codes

5. Always read documentation for API's

6. Make application get data from API- Add function to controller
   export class SwapiController{
   constructor(){
   this.getPeople()
   }

async getPeople(){
try{
await swapiService.getpeople()

    } catch(error){

    }

}

}

7. Go to service and make async getpeople()

class SwapiService{
async getpeople(){
const response = await axios.get('link of api')
IMPORTANT/log the res!!- console.log(response.data);
let people = response.data.results
}
}

7.5 Add axios cdn link to bottom of body, which is a library that makes requests easily
import axios to service layer

8. app state- people= []

9. Add in HTML

10. go to controller add proxystate.on to constructor, add function drawPeople()

------2/22/22 GregsList API----

1. Add axios to HTML

2. new service AxiosService.js, export const api = axios.create({
   baseUrl: 'https://bcw-sandbox.herokuapp.com/api',
   timeout: 8000
   })

3. Go to Service, add method to Service class
   async getAllCars(){
   const res = await api.get('cars')
   console.log('get all cars', res.data)
   ProxyState.cars = res.data.map(rd => new Car(rd))
   }

4. query parameter- ?make=chevy which would be all chevys or whatever make may be

5. Go to controller async vewCars(){
   try{
   await carsService.getAllCars()
   document.getElementById('modal-body-slot').innerHtml = getCarForm()
   document.getElementById('create-button').innerHtml = getCarForm()
   } catch(error)
   }

6. Go to Model

7. Going forward no more generateId()

8. Get form to work, go to service, add async to createCar(){
   //delete other stuff
   const res = await api.post('cars', newCar)
   log('[CarsService:] createCar', res.data)
   let car = new Car(res.data)
   ProxyState.cars = realCar, ...ProxyState.cars

}

When getting 400, go to network tab, click and read, view payload

9. PUT
   Edit button, add button to template
   go to form, rename method to handle submit in the onsubmit of form class, go to controller and change create to handleEvent()

change getCarForm - (carData)

--------------2/23/2022 Spells API---------------

1. Hook up axios, make axios service

2. Create controller DndSpellsController, export class, make constructor, console.log

3. Make Service, DndSpellsService, make class, export const

4. Make one Model, Spell.js, will be used for spells from api and sandbox server, export class spell

5. Bring controller into main.js

6. Go to controller, make a
   async function \_getSpells(){
   try{
   await dndSpellsService.getSpells()
   }catch(){
   }
   }

7. Go to Service, import axios, make async getSpells(){
   const res = await dndApi.get()
   console.log('[getSpells]', res.data)
8. ProxyState.dndApiSpells = res.data.?Check console
   }

9. Go to AppState, dndApiSpells = [], mySpells = []

10. Gp to controller, make draw
    function \_drawSpellsList(){
    let templayte = ''
    ProxyState.dndApiSpells.forEach(s => template += `<li class="selectable" onclick="app.dndSpellsController.getActiveSpell('${spell.index}')> ${s.name}</li>)
    document.getElementById('api-spell-list').innerHTML = template
    }
    go to constructor in controller, make listener

11. Make HTML template, change div id to api-spell-list

12. Go to controller make onclick above then
    make async getActiveSpell(index){
    try{
    console.log('getting active spell', index)
    }catch(error)
    }

13. go to api and figure out index for spell so onclick will give info of spell

14. Add index to active spell above as well as to the onclick

15. Service, async getActiveSpell(index){
    const res = await dndApi.get(index)
    log('[getActiveSpell]', res.data)
    }

16. Make class Spell model in Spell.js

17. Go to AppState and make activeSpell = {} not []

18. G to servive and add to active spell function
    ProxyState.activeSpell = new Spell(res.data)

    19. Go to controller make \_drawActiveSpell(){
        document.getElementById('active-spell').innerHTML = ProxyState.activeSpell.Template

    }

    20. Make Template for active spell, div id active spell, put get template function in model, add template, add string interpolation

    21. Register listener for active spell

    22. Make next controller MySpellsController.js, make export class

    export class MySpellsController{
    constructor(){
    log('')
    }
    async saveSpell(){
    try{
    await mySpellService.saveSpell()
    }catch(error)
    }
    }

    23. Make class MySpellsService(){
        async saveSpell(){
        let spell = ProxyState.activeSpell
        const res = await sandBoxApi.post('', spell)
        log(''[saveSpell]', res.data)
        }
        }

    24. Hook up in Main

    25. export const sandBoxApi = axios.create.....

    26. Go to new controller make method in class Controller

    27. Make onclick in template app.mySpellsController.saveSpell()

    28. use .join to turn into string from array

    29. MySpellsController
        async function \_getMySpells{

    }

19. MySpellsService
    async getMySpells(){

}

31. MySpellsController, make \_drawMySpells

32. make new template for MySpells, get ListTemplate

33. Go to controller, make setActiveSpell(id){

}

34. MySpellServive make setActiveSpell(id){

}

35. Add to model get Button(){

}

36. make removeSpell(){ on controller and service

}

37. HTML- input type ="checkbox" ${this.prepared ? 'checked' : ''} onclick="app.mySpellsController.prepareSpell()"

38. Add prepareSpell() to controller

39. Add prepareSpell() to service

40.

41.

42.
