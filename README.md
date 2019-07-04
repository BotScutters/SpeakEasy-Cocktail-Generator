## SpeakEasy, the AI Bartender

Author: Scott Butters

Description: This is a deep learning framework that integrates knowledge about cocktails and their ingredients with a natural language understanding of English to invent and suggest cocktail recipes in response to a plain English requests.

You know that thing where you're hanging out in a schmancy speakeasy and the bartender asks you what you'd like to have—not in terms of a specific cocktail, or even the base spirit, but in terms of the flavor profile? And then just sets to work grabbing one bottle after another until before you know it you've got a little bit of magic in your mouth and you don't even know how? That. That right there is the epitome of mixology, as far as I'm concerned. That's "[the speakeasy experience](http://speakeasy-ai-bartender.herokuapp.com/)." That's what I've sought to recreate with this app.

<figure>
  <img src="/reports/bar.jpg" alt="speakeasy-bar" style="width:100%">
  <figcaption>My home bar, soon to be tended by my personal AI assistant.</figcaption>
</figure>

# Abstract

[The SpeakEasy app](http://speakeasy-ai-bartender.herokuapp.com/) is a cocktail recommendation engine that's built to transform plain English requests from a user into a suggested cocktail that best matches the request. The functionality of this system rests on three systems:

- A database of cocktails, containing recipes, descriptions, and metadata for each.
- A model trained to vectorize and transform text describing a cocktail into an appropriate topic space.
- An app that uses the model trained on the cocktail database to make new predictions based on user's request.

The first production version of the app is making use of cocktail data scraped from [Difford's Guide](https://www.diffordsguide.com/cocktails). The text data from each cocktail is processed into a document-term matrix using a TF-IDF vectorizer, then factored into a document (cocktail)-topic matrix using latent semantic analysis (LSA). Finally, the data, vectorizer and LSA transformation matrix are packaged into a Flask app and hosted on Heroku so all the world can get the drink they're itching for.

The code for both the [SpeakEasy modeling](https://github.com/BotScutters/SpeakEasy) and [SpeakEasy app](https://github.com/BotScutters/speakeasy-app) are available on my [GitHub](https://github.com/BotScutters).