---
title: lang-python-community-proposals
tags: [community, proposal, python]
created: 2025-09-06T10:32:58.004Z
modified: 2025-09-06T10:33:19.831Z
---

# lang-python-community-proposals

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-types
- ## 

- ## 

- ## 

- ## [In which cases are dicts preferred to dataclasses? : r/learnpython _202312](https://www.reddit.com/r/learnpython/comments/1898vlx/in_which_cases_are_dicts_preferred_to_dataclasses/)
- If a dictionary will do the job, then it is usually the better choice, though in some cases using a dataclass can significantly improve readability.
  - If you need "methods", then a class or dataclass is likely to be the better option.

- Pythonistas tend to use dicts and lists for just about everything, and only move to custom classes when necessary. This is opposed to something like java, where the idiomatic thing is to make a class upfront for everything.

- One reason is separation of data and code. Use dicts when the keys are part of the data. Use dicts when the "keys" (or attribute names) are meant to be code.

- Whenever the keys are not constant or are other hashable types, like tuples.

- a dict for when you make one object, and you use it for looking things up. "Map" really does describes the job better
  - a dataclass (or some kind of class) when you're gonna make a bunch of objects. Accessing attributes with a dot really is better than brackets

- ## [Should I use pydantic for all my classes? : r/Python _202404](https://www.reddit.com/r/Python/comments/1c9h0mh/should_i_use_pydantic_for_all_my_classes/)
  - Perhaps it's because I'm not using it correctly but my code for a pydantic class is much longer then for a normal class. Especially if you are working with computed attributes. Then you have to start using special decorators and for every computed attribute you have to declare a function with "def ..." Instead of in an init function just being able to write attribute_3 = attribute 1 + attribute 2.

- No, I don't. I only use pydantic to validate user input, such as when building an web API. The user might send some json data, and I use a pydantic class to validate that the data received contains all the required arguments with the correct types.
  - When coding things that are for my use or my colleagues use, I use type hints but not pydantic.

- Agreed, type hints + mypy is enough and faster. I am still using pydantic instead of dataclass though when I just want a struct of data.

- Why pydantic, why not marshmallow. Marshmallow can act as a validator and serializer. Genuine question
  - If you use pydantic as a Base you're all set to use Fastapi, fastui, combadge, so many awesome tools you can just specify pydantic models as inputs or outputs. 
- FastAPI uses Pydantic model validation. but all of the things you said can be achieved in Marshmallow. 
  - They're integrated tools. Pydantic + Fastapi + sqlmodel + Fastui is a stupidly useful stack that all just works together nicely. 

- 👷 I'm working at Pydantic, the company. Samuel Colvin is my boss. Many of the classes in our codebase are pydantic models, but most are not. There's more dataclasses than pydantic models, and there's also plain standard classes.
- why would I use a dataclass over a pydantic class? 
  - Some inner parts of the model may point to the same object in memory as in the original data, but not all of it, so there's definitely some overhead. Whether or not it's an amount that matters will depend.
  - When you don’t need the inputs validated to your class. Imagine converting a DTO object that represents your result from an API into a class that your business logic uses. All your data validation occurs in the DTO, so adding the runtime penalty of checking again when creating the business logic object is unnecessary
- We'd have to add `arbitrary_types_allowed=True` all over the place, and it'd probably also be inconvenient in other ways.

- Pydantic for JSON data received from outside, dataclasses for everything else

- I like msgspec for message deserialization and type validation. Most of the time Pydantic is overkill. Msgspec is fast and the Struct classes work well.

- Pydantic is for user input validation -- it's just needless overhead for internal classes.

- Pydantic doesn't make your code any more strongly typed than dataclasses do. Its just a library to handle more complex serialization and validation concerns.
  - TL; DR use the right tool for the right job. 
  - Validation and parsing? Sure. 
  - Internal models? There is zero benefit of the overhead. Use named tuples and/or dataclasses based on what you need. 
  - For internal service to service communication, using something like protobuf will be beneficial as a contract.

- ## 🆚 [Pydantic vs TypedDict — My Experience Choosing Between the Two _202507](https://medium.com/@ansurkar.tejasvi12/pydantic-vs-typeddict-my-experience-choosing-between-the-two-bbbdcb9275fd)
- both involved type hints, and both had some form of structure. 
- But after digging deeper, I discovered that they serve two very different purposes
  - TypedDict is like writing down rules on paper and hoping everyone follows them.
  - Pydantic is like having a bouncer at the door checking if your data meets the rules before letting it in.

```markdown
+----------------+--------------------------+---------------------------------+
|    Feature     |        TypedDict         |            Pydantic             |
+----------------+--------------------------+---------------------------------+
| Type checking  | Static only (during dev) | Happens at runtime              |
| Validation     | Nope                     | Yes — it even converts types    |
| Performance    | Super lightweight        | Slightly heavier due to parsing |
| Default values | Not supported            | Fully supported                 |
+----------------+--------------------------+---------------------------------+
```

- TypedDict
  - Python won't complain — unless you're running a type checker like mypy. And even then, it's only a warning.
- pydantic will happily convert the string "30" into the integer 30

- TypedDict is perfect when:
  - I'm working with internal data structures that don't need validation.
  - I want lightweight code with better IDE support.
  - I'm okay with relying on static tools like mypy or pyright.

- Pydantic shines when:
  - Data is coming from the outside — an API, a form, a JSON file.
  - I need to validate, coerce, or transform data before using it.
  - I want to write cleaner, safer code without adding tons of manual checks.

- I actually started using both together. I define my dictionary shape with `TypedDict`, use it in functions for static hints, and pass it into a `pydantic` model for parsing when needed.
# discuss
- ## 

- ## 
