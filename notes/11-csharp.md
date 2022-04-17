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

-------SECTION Monday Icats Interfaces and Inheritance-----

1. Make a folder called interfaces. interfaces are a way to add structure and scaffolding to your project before you start building your app. A way to create standards for your application.

namespace ?.Models
{

When people interact with each other they will be seeing profiles not account but if you are the account owner, when you request account info it will show Profile and account info

public class Profile{

public string Id {get; set;}
public string Name {get; set;}
public string Picture {get; set;}

}
The account inherits from profile
inherits, pulling info from accounts model but only send back the profile info when a different user is accessing
public class Account : Profile
{
public string Id {get; set;}

// Sensitive Information on account that you don't want to get back
public string StreetAddress {get; set;}
public int CreditCardNumber {get; set;}

}

}

1. Make interface folder, Add interface file IRepoItem.cs

namespace Icats.Interfaces
{
public interface IRepoItem<T>
{
public int Id {get; set;}
public DateTime CreatedAt {get; set;}
public DateTime UpdatedAt {get; set;}
}
}

2. Go back to account.cs and make Profile : (inherit) IRepoItem.
   Add Id, createdAt and UpdatedAt on to the profile model
   Profile can now be a repo item because it now has those props from IRepoItem

3. Add new interface file IRepository.cs

namespace Icats.Interface
{
public interface IRepository // this is what makes up repository layer/ shows that this is what makes up a repository
{
List<Profile> GetAll()
Profile GetById( string id);
Profile Create(Profile data);
Profile Edit(Profile data);
string Delete(string id);
}
}

4. Make profiles repository and have it : (inherit) the IRepository

namespace Icats.Repository

How to make interface not care about the Id datatype, whether its a string or an int

Use T in front of all propes and add <T> to the interface and then throughout the models specify in inhertance <> what the id will be
Example public class Cat : IRepoItem<int>
{
public int Id {get; set;}
}

------ 4/12/2022 Many to Many Front end-----

1.  <!-- Many to many table -->

        warehouseProducts(

    id INT AUTO_INCREMENT PRIMARY KEY,
    warehouseId INT NOT NULL,
    productId INT NOT NULL,
    FOREIGN KEY (warehouseId) REFERENCES warehouses(id),
    FOREIGN KEY (productId) REFERENCES products(id)
    ) default charset utf8 COMMENT '';

2.  Delete with foreign key constraint. Add ON DELETE CASCADE to the warehouseId and productId in the many to many table. If not written before creating table, must drop table first.

3.  Add public class ProductViewModel : Product in product model. ViewModel means what the front end will view, how do you want to view this data in the front end?
    {
    public int WarehouseProductId {get; set;}
    public string Location {get; set;}

}

3. WareHouseProductController
   Build the create method
   Add [HttpPost]
   public ActionResult<ProductViewModel> Create([FromBody] WarehouseProduct warehouseProductData)
   {

}

4. Make Create in service pointing to repo
   <!-- Making the switch of data types in service -->

   {
   WarehouseProduct warehouseProduct = \_repo.Create(warehouseProductData);
   <!-- Making the switch -->

   ProductViewModel product = (ProducViewModel)\_pService.GetById(warehouseProduct.ProductId)
   Warehouse warehouse = \_wService.GetById(warehouseProduct.WarehouseId)
   <!-- Adding view model properties/ location and warehouseProductId -->

   product.WarehouseProductId = warehouseProduct.Id;
   product.location = warehouse.Location;
   return product;

   }

5. Make Create in repo

internal WarehouseProduct Create(WarehouseProduc warehouseProductData)
{
string sql =@"
INSERT INTO;

     int id = _db.ExecuteScalar<int>(sql, warehouseProductData);
     warehouseProductData.Id = id;
     return warehouseProductData;

}

Object reference not set to an instance of an object postman error
You're referencing something that has not yet been created

1.  computed to get warehouses on to homepage

2.  make new component warehouse.vue

3.  bring in warehouse component to homepage, make v-for on col above <Warehouse /> for tiling

4.  Add props onto warehouse component

5.  where to put modal when wanting to click on warehouse and open showing packages within the warehouse

6.  Put it at the bottom of template on homepage

7.  <Modal id="warehouse-modal">
       <template #modal-header>{{activeWarehouse}}
       </template>
       <template #modal-body>
       <WarehouseDetails />
       </template>
    </Modal>

    add data-bs-target and toggle to selectable add setActive()
    in script in return make a method for set active

    Add computed for activeWarehouse

    make getAll in warehouses service

    make getproducts in warehouseService

    make a computed in warehouseDetails for products to be able to access them in template

    make another component product.vue

    make v-for for Product component in warehouse details

    in product.vue add props for product

    <Product> is the child of warehouseDetails so the props go in to the Product Component and the computed goes in to WarehousesDetails component

    Add computed to home page for products after bringing in <Product> props still only on Product.vue

    8.  Now showing a seperate modal for each product
        Add modal to product.vue with product.name and product.description and product.sku

    9.  To take product and put into warehouse
        On Product.Vue make a drop down <select name = "" id="">
        <option value = ""> option 1</option>
                           button with @click addToWarehouse()

8.  Add computed for warehouses on Product.vue to be able to access them. Add v-for on option for your warehouses
9.  when accessing ref in script you must use value

---- Many to many groups----

1. You can set up a private method in membership service for get(id)

2. To be able to get to your groups from any page
   Go to authservice, groupsService.GetMyGroups
   make that method in groupsService
   make myGroups in appstate as to not reuse groups
   Dump my groups into homepage

----All day code---

1. Add uniqueness to all of your exceptions
2. FirstOrDefault for one, ToList for more than one in repo
3. Use just GetById in your update and delete in service because your GetById in service has a check on it
4. 405 in postman means the route exists but the method does not exist on that route
5. Makes profile controller to get the reviews that profile has made
6. If sending a method to a service of a different type (sending from profile controller to review service), specify the id as profile id in review service
7. If creatorId is ambiguous you must check to see if both tables have the same column, must specify which
8. If grabbing full info from both or more tables when joining, you must map.

-----Client-----

1. Get rid of all prebuilt stuff
2. Add setup to homepage, make your onMounted in that set up, put in your try catch, make your service, back to homepage, make your getall calling to service. back to service, make your get all in service. put whatever youre calling into appstate, make your return and add computed for what you were getting.

3. Add container to div class to template on homepage, make a row, make a col, add v-for to that col, test with data dumps of name. Add styling. Make card. <img class="img-fluid" :src="?.picture"/>

4. Object-fit-cover in css to make the picture fit and cover

5. Use span tags to keep things together when styling but want to push something else to the end

6. Clean up all styling and data from home and make a new component, add props to that component that you made to be able to inject to another page.
   Inject <Restaurant /> into Home

7. Make @click in component. Add setup and return to script. make setactive in return, add active to appstate. pass props through setup.

8. Make Modal component. bs5-modal-default. make slots with name for title and body. modal-xl, to vertically center modal on page add modal-dialog-center in dialog div

9. Add data-bs-target=#id, data-bs-toggle="modal" to component where the setactive is

10. Make details component. Put Modal into this component dump data, throw computed for active? in return

11. Put <Details> in App.vue in routerview tag

12. Style details component where modal content lives, add all details {{}}

13. Make get method and point to service for details in the page holding setactive @click. Add close modal as well.
    make method in service to get what you are looking for. Add computed in page with setactive, dump data

14. Add ? mark after anywhere you are drilling more than twice when calling to data in case its calling for something that isnt there yet.

15. Clean it up

16. Make Profile Page.

17. Use router link for icon use go to on modal so that it closes it at the same time

18. In details component, add gotoprofile and add in the Modal close and router push. In setup add const router.

19. On profile page add all infor needed, add onmounted, write new service for profiles, back to profilepage, point to service wiith addprofile and addreviews add in route.params.id to get id, add use route in set up to get route. Make methods in service.

20. Add data to template in profile, add computed

21. review count on profile page {{reviews.length}}

22. average for reviews add method into return averagereviews:computed(()=> {
    let total = 0
    reviews.foreach(r=> total += r.rating)
    return (total / reviews.length).toFixed(1)
    })
23. {{averageRating}}

24. NO D-FLEX ON MASONRY INCLUDING ROWS. ROW HAS D-FLEX.

25. How masonry works:
    in script on profile page
    Add class on parent div.
    add css class masonry-with-columns {
    columns: 6 200px;
    column-gap: 1rem;
    div{
    display: inline-block;
    width: 100%
    }
    }

v-model goes goes on input for form. Add ref in same page under set up where v-model is located. use .value with ref
