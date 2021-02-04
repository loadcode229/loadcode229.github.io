---
layout: post
title:      "Mod 4 Project (Recipe Manager)"
date:       2021-02-04 00:07:54 +0000
permalink:  mod_4_project_recipe_manager
---

The github link: https://github.com/loadcode229/recipe-manager

Being much more comfortable with building these sorts of projects, I was able to focus a lot more on the frontend of the project more and really understand the code from point A to Z.

# Project:
The backend was built using Rails and the frontend used JavaScript/CSS/HTML.

In our backend, we had 2 models: User and Recipe.

Our app flow is like so:

1. You must create a User.

2. Once created, you can add a recipe to that user.

3. You can select a user to view their created recipes.

4. You can 'Like' the recipes you've created, as well as 'Reset' that like if you change your mind or something. 

5. You can delete that user's recipes.

Building out the recipe card to work and look properly was definitely the biggest challenge working on this project.

In order for the card to render properly, I had to layout the HTML of the card and append each variable in the order I want my user to view it.

Appending each variable in order of user viewing:
```
        divCard.append(h2, h4, tbody, p, likeBtn, resetBtn, deleteBtn)
```







