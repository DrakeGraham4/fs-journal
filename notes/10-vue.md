# MVC

------Art Terminal----

1. Getting projects to home page

- Renamed account page to Profile Page, account would always be you, profile page would be others.
- Home button should show all projects
-

2.  Start in HomePage.vue, make a setup() and onMounted
    to make network request. Make try catch. Make a request.
    await service.getAll()

3.  Make get request in service from Api to get all posts

- log the res to see if you are getting projects in logger. Add AppState.projects = res.data to getAll func, no map if not using query.

4.  Make AppState

5.  Check vue tools to see if data is in AppState, if vue doesnt show up try closing browser and reopening or respinning project

6.  To get projects on HomePage make a template. Make col-md-6, make main div container-fluid. put computed in return. put v-for and :key in col div.

7.  Make Project.vue in components.

8.  Add <Project :project = p /> to homepage

9.  Add Props ro Project.vue under export default.
    props:{
    project: {
    type: Object,
    required: true
    }
    }

10. Make template for what project should look like in Project.vue
    use row because there is a column in HomePage, check res.data in log to see what injection to use in template. Use :src in image tag to bind the info.
    Add img-fluid.

11. Make Modal.vue, under components to view. Use bs5-modal to make modal quickly. Add Modal to onclick on picture. Add Modal to App.vue under main.

12. Add slots to modal in Modal.vue

13. In App.vue add in slot template between Modal tags

14. Each page has to be self-sufficent, it has to get the information that it is trying to display. That's why get one and get all are on seperate pages. Since there is no page details component and only when you click and open modal with ones details,
