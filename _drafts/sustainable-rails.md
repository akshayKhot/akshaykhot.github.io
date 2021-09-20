To sustain the development of our software is to ensure that it can continue to meet its needs. A sustainable software handles new requirements, increased demand on its resources, and changing team of developers to maintain it. 

Sustainable software minimizes the cost of developing and maintaining software over time. Working on sustainable software is more fun. 

- The software has a clear purpose
- Software needs to exist for years
- The software will evolve
- The development team will change

It is a good practice to document why gems are there and what they do. Ruby gems don’t have a great history of self-explanatory naming, so taking a few seconds to document what a gem is for will help everyone in the future when they need to understand the app.

---

**Routes**

Stick to the most basic features of the Rails router. It means anyone can easily understand your routes, and even the most inexperienced developer can begin adding features. This is sustainable over many years. 

- Always use canonical routes that conform to Rails defaults.

- Never configure routes that aren't being used. Use `:only` flag to restrict. 

- Vanity URLs should redirect to a canonical route. 

- Don't create custom actions, create more resources.

- Resources should never be nested more than one level deep.  

---

**HTML Templates**





