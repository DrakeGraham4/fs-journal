# MVC

DLL file

dotnet new to start a new project, console app

dotnet new console -o funner_sharp

-----Gregslist C# Web MVC-----

command to fix certificate error in slack

appsettings are equivalent to env.js

route is just like super in controller [Route("...")] which is the route to your public class underneath

spin up, .NET Core Launch, there is no built in default base route, to check add api/weatherforecast to url, use /swagger to see documentation and use their postman like tests.

Writing your own controller
SECTION

1. Start with Models/ Add Services/ DB add class called fakedb
2. Make a model for whatever you're making in this case cat, make your auto props. Add = guid- globally unique id on public Id
3. Add constructor only because we are using fake DB
4. Go to FakeDB add static to public class FakeDb//public static class FakeDb FAKEDB IS TODAY ONLY
5. Add auto props to FakeDb class public static List<Cat> Cats {get; set;} = new List<Cat>(){
   new Cat("Dudley", 1),
   new Cat("Falcon", 2)
   }
6. Jump into controller, make a controller for your item / Cats in this case. Add namespace with ; at the end
   make public class/ all controllers will be public. public class CatsController : ControllerBase. Add [ApiController] above add route above [Route("/api/[controller]")]
   Within public class Add [HttpGet] beneath add public ActionResult<List<Cat>> Get() No res.data, just return Ok

7. Test in swagger, will auto figure for the code you've written. Copy and paste route in swagger add to url and see for yourself

8. Pass method into service. No such thing as export so make the service, in program.cs add builder.Services.AddTransiet<CatsService>();

9. Add to controller within class, private readonly CatsService \_cs; underneath public CatsController(CatsService cs) {\_cs = cs}

10. Take out Ok return in Get add List<Cat> cats = \_cs.GetAll();
    return Ok(cats)

11. return FakeDb.Cats in service

12. Check in swagger and new url

13. Most common error and how to solve it, if you forget transient swagger will still spin up. if you forget transient you will get huge error unable to resolve. Failed Microsoft.Extensions.DependencyInjection

14. Don't forget to wrap methods in try catch in controller

15. Add getById in controller in csharp its {id} rather than "/:id"
    to get param id it's getById(string id) rather than route.params.id/is just a parameter on the method now

16. Generate method in service, write service method

17. Handle bad request in service, add if statement

18. Add delete to controller, add delete to service. Use void because deletes don't return

19. Make create in controller. req.body is now [FromBody] so its Create([FromBody] Cat newCat)

20. Make create in service

21. Test in Swagger

22. Handle things you don't want to happen. When you create a cat you have to have a name. Add [required] in Cat Model above name, only counts for the immediate attribute. Add paramters for age for numbers [Range(0, int.MaxValue/whatever you want the max to be)]. You can also add [minLength] for name or characters

23. Make update in controller, will be combination of get and post.

24. Make update in service

SECTION----BurgerShack SQL----

1. Start with model, use double for price. Use = "No description required" if you want to set a default on a description

2. Make Controller, make your CRUD methods. GetByIds will be int ids. In your post method use return Created($"api/whatever/{whatever.id}", whatever) for a restful/fancy API.

3. Add transient in startup.cs line 44

4. SQL / MS-SQL - relational database / data stored as tables
   MYSQL
   POSTGRESS

5. MongoDb- NoSQl/ Document Database/ data stored as objects

6. In appsettings.development/json add connection string and auth stuff

7. dbSetup.sql, add in your tables before you can spin up project in swagger

8. Create repository

9. Service Layer will send to repository layer. Import repository into service just like you did the service into the controller

10. Make service methods

11. Make methods in Repository

12. spin up new bcw create, copy and paste controller, change namespace, rewrite service

SECTION-----Thursday SQL Review-----

1. Build Model. to make a one to many with an account

2. Build dbSetup, look for the 3 stack at bottom to see if you're connected. \* is give me all columns from games. Add to table//Update table games, add column creatorId varchar(255) not null foreign key(id) accounts;

Any time there is a promise/async on methods you must use Task<ActionResult<Game>>, also use [Authorize] under your [Http?].

----SECTION Many to Many----

1. Make Model
   public int Id
   public int GameId
   public int Score

2. Create table for your many to many
   id INT AUTO*INCREMENT primary key
   gameId INT NOT NULL
   accountId VARCHAR(255) NOT NULL
   score INT DEFAULT 0
   // Because many to many, make foreign key
   FOREIGN KEY (gameId) REFERENCES game(id) ON DELETE CASCADE // if you delete game the score will also delete
   FOREIGN KEY (accountId) REFERENCES accounts(id) ON DELETE CASCADE // if you delete an account the score will delete as well
   CREATE 3. Make INSERT INTO gameplayers
   (gameId, accountId, score)
   VALUES
   (1, "6234ksdnvodv905", 300);
   GET ALL
   SELECT * FROM gameplayers;
   GET BY
   SELECT \_ FROM gamplayers WHERE accountId = "6234ksdnvodv905";

   SELECT
   a.name,
   gp.\*
   FROM gameplayers gp
   JOIN acccounts a ON gp.accountId = a.id
   WHERE gp.gameId = 1; // this will get you the name of the account and all information of gamePlayers for game 1

   SELECT WITH GAME NAME
   a.name,
   a.picture,
   gp.score,
   gp.id AS gameplayerId
   FROM gameplayers gp
   JOIN acccounts a ON gp.accountId = a.id
   WHERE gp.gameId = 1; // this will get you the name of the account and all information of gamePlayers for game 1
   this will give you a table with the account name, the account picture, the score of the gameplayer tied to that account, changes the gp to gameplayerId, joins the gameplayer table to the account table, and shows their information for the gameid 1.

3. To get my games/favorites, you must go through accounts controller and make get request. must add private readonly for GamesService to be able to call it in accounts controller.
4. Set up method in GamesRepository. Also must at score and GamePlayerId to Game model if wanting to send score back to client.
