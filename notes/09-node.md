# MVC

-----Week 5 Node-----
Use bcw create, select node-server

main.js is entry point of application

The super comes in when there is inheritance

req always represents the knight as he comes in with a request, res always represents the knight coming out

The information that the knight came with is always the body

Mongo holds data, mongoose translates data back and forth

Express is the server library

Node does not need .js

always req, res, next

if you change something you must restart server with green arrow above

export class CatsController extends BasController{
constructor(){
super('api/cats')
this.router
.get('', this.getAllCats)
.post('', this.createCat)
}
}

async getAllCats(req, res, next){
try{
let cats = await catsService.getAllCats()
return res.send(cats)
} catch (error){

    }

    async createCat(req, res, next){
        try{
            console.log(req)
            const cat = await catsService.createCat(req.body)
        } catch(error)
    }

}

Go to CatsService

class CatsService{
async getAllCats(){
const cats = await dbContext.Cats
return cats
}

}

export const catsService = new CatsService()

Go to dbContext
Cats = [{name: 'Mr. Snibblysmith, color: 'Orange'}, {name: 'Madam Blackwell'}]

Go to play button and hit Start Server, go to local host port by typing it into web address, append end point localhost:3000/api/cats

Use postman use get

after

------------3/1/2022------------

Make Create Car in postman, make sure using raw and JSON

post and put are the only thing with a body. get and delete do not have a body

type into body what you want
ie "make": "HoHum",
"model": "V",

    Essentially the decree of that is sent with the night/rec.body

    Add use to super to make sure they have to be logged in

    constructor(){
        super('app/cars')
        this.router
        .get('', this.)
    }
