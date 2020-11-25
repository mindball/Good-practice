# Architecture with service layers
## Scenario: have two services in this layer - ItemService.cs and CategoryService.cs
```
The database contains the many-to-many relationship between Item and 
Category. If I want to add the following function: AddCategory(int itemId, Category category) 
what is the (most) suitable place in your opinion - the category service or the 
item service? To which context this function relates most?
```
## Opinion:
```
In reality - it could be both. But considering the fact, that you have in the method 
definition AddCategory only the Id for the Item and the full object for the Category, 
then I would put it in the CategoryService. Usually - objects which are not part of the 
current "context" (in this case the service), should be referenced by Id only. 
When you use the full reference object - the category, then it means that it is in 
the same "context". Is my answer clear enough? Here are some examples:
- AddCategory(Item item, int categoryId) - put it in the Item service.
- AddCategory(int itemId, Category category) - put it in the Category service.
- AddCategory(int itemId, int categoryId) - both services are correct.
- AddCategory(Item item, Category category) - unnecessary references, too much information in the method signature.
```