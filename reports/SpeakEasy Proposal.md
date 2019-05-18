# SpeakEasy, the AI Bartender

*Scott Butters*

You sidle up to the bar at a schnazzy speakeasy downtown and the bartender asks you what you're feeling like. "Oooh, I don't know..." you say, "can you give me something that's like a margarita, but…spicy? Oh, and smoky, but not too sweet."

"I know just the thing," the bartender says. He gets to work grabbing one bottle after another of things you've never heard of before, and a moment later you've got a bit of magic in your mouth, somehow exactly what you'd just asked for. 

That kind of bartender is a special find, a true mixologist. But can we get that kind of thing in the comfort of our own home? Introducing:

## The Natural Language Purveyor of Cocktails

SpeakEasy will be a framework that integrates knowledge about cocktails and their ingredients with a natural language understanding of English to suggest and invent cocktail recipes in response to plain English requests. The prototype will be served up as a flask app hosted on Heroku.

While the front-end will be simple to interact with, the system will house three major components under the hood:

* An engine for tokenizing plain-text descriptions of cocktails into a machine interpretable design matrix
* A separate system for parsing cocktail recipes into a desciptive design matrix.
* A model trained to transform a description-space input to an ingredient space output

## Data Sources

There are many potential sources of data for this project, each with it's own pros and cons. Below is a list of websites that each offers (at a minimum) hundreds of different cocktail recipes and (at least for many of them) descriptions to go with.

* [The CocktailDB](https://www.thecocktaildb.com/)
* [The Spruce Eats](https://www.thespruceeats.com/a-to-z-cocktail-recipes-3962886)
* [Drizly](https://drizly.com/recipes#all-recipes)
* [Kindred Cocktails](https://kindredcocktails.com/cocktail?scope=0)

By scraping these and maybe more websites for cocktail information, we should hopefully be able to compile description and ingredient data on somewhere in the range 1000 or more cocktails.

## Methods

### Tokenizing Descriptions

To tokenize the descriptions, I'll likely make use of tools such as NLTK, Gensim, and SpaCy. I'll remove stop words, tokenize various ngrams, extract named entities, and maybe more. In ideal form, the description engine will leverage pre-trained models to recognize words with similar meanings as well as effectively recognize and respond to requests and negations (i.e. distinguish between "with tequila" and "no tequila").

### Tokenizing Recipes

The recipes should be marginally easier to represent than the descriptions, as there is some inherent order. I expect to have a column for every potential ingredient, as well as a few others for things like whether or not the drink is served with ice or in a particular type of glass. Liquid ingredients will have values representing the prescribed volume to add, and columns representing ice, glassware, shaken/stirred, garnish, etc. will be represented as booleans.

### Tying the Two Together

At the heart of SpeakEasy is a transfer function which allows us to convert a vector from desciption space to ingredient space. I'm not entirely certain yet of what model will give us the best version of this transformation, but my thinking is that it will likely be a neural network with an equal number of output neurons to the number of columns in the ingredients matrix. In ideal form, the system will be built such that the model always outputs:

* At least 2 but no more than 8 ingredients
* Minimal overlap of ingredient class (i.e. don't suggest two different types of bourbon in the same recipe)
* Glassware type

### User Interface

The baseline interface I'd like to built is a flask app with a text box for input. A user can enter whatever input they desire into the text box and the model will generate an output to match. For my MVP, I'll have the model select an existing cocktail that most nearly matches the request, but as an extension I would like to add the ability for the model to interpolate between recipes and invent new cocktails for each request.

To guide the user's choices, I will offer some suggestions on the page of types of inputs that may yield better results.

## Known Challenges

There are many. For starters, the data will no doubt be very dirty. It will definitely be a challenge to collect both ingredient and description data for enough cocktails to build a well-behaved model. Next, getting the model to effectively generalize and understand such things as flavor profiles and similarity of ingredients is something I expect to be a problem. Handling the fact that some recipes call for brand-specific ingredients of a broader category will be a challenge. Effectively responding to complex user input like requirements and negations will also be a challenge.