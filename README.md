# FRONTEND ARCHITECTURE NOTES

## FOUNDATIONS

### DEFINITION

Set of **significant decisions** about how the software/Frontend is
**organised** to promote desired **quality attributes** and other **properties**

### DIMENSIONS

#### STYLE

- Microservices
- Monolith
- Single Page Application
- Multi Page Application
- Layered Architecture
- ...

#### CHARACTERISTICS

- Performance
- Security
- Maintainability
- Testability
- Portability
- Scalability
- All the _"ilities"_

#### DECISIONS

- Structural guidelines
- Naming conventions
- Code structure
- Dependencies
- Data flow
- Error handling
- Logging
- Testing
- Documentation
- Versioning
- ...

#### LOGICAL COMPONENTS

- Modules
- UI Components
- Design System
- ...

**Example:**
| Dimension/Architecture | Architecture 1 | Architecture 2 |
| ---------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Style | Microfrontends | Monolithic RSC |
| Characteristics | Scalability, Deployability, Maintainability | Performance, Agility, Reliability |
| Decisions | Share global state with signals, compose Microfrontends client-side | Share global state with a store, mutate data with server actions |
| Logical Components | Models, Collections, Templates, Classes | Client components, server components, hooks, services |

### FRONTEND VS BACKEND

Frontend → **HTML, CSS** → **Next.js / React Native** → **Database / API** ← Backend

### ARCHITECTURE VS DESIGN

Structure → **Architecture** - **Design** ← Code

#### ARCHITECTURE

- Hard to change
- Strategic (involve teams)
- Higher level
- **Example**: Define style (Microfrontends, Monolithic RSC)

#### DESIGN

- Easy to change
- Tactical (involve a single team)
- Lower level
- **Example:** Share global state with signals

### ARCHITECT ROLE

#### SETTING TECHNICAL DECISIONS

- Create technical vision & strategy
- Align the team on the vision & strategy
- Making architectural decisions
- Writing and reviewing code

#### APPLYING ARCHITECTURAL THINKING

- Understanding and analysing trade-offs
- Understanding business drivers & translating them into architectural decisions
- Having wide breadth of tech knowledge and having tech deepth

                Technical breadth

                      /\
                     /  \
                    /    \
                   /      \
                  / Stuff  \
                 /   you    \  Technical depth
                /    know    \
               /______________\
              /                \
             /      Stuff       \
            /   you know that    \  Focus on this → Expand your knowledge.
           /    you don't know    \                 Achieve good understanding.
          /________________________\
         /                          \
        /           Stuff            \
       /     you don't know that      \
      /          you don't know        \
      \________________________________/

#### DOING GLUE WORK

- Writing docs
- Running meetings
- Mentorship and sponsorship

## UNDERSTANDING

### C4 MODEL

C4 models are a set of diagrams that help you to understand the architecture of
your system

#### SYSTEM CONTEXT

- The big picture of the system
- It does not change over time

![system-context](https://tinyurl.com/3826mpck)

**Example:** The system context of a banking application

#### CONTAINERS

- A container is a logical grouping of components (applications and data stores)
- It zooms in one of our system contexts
- It barely changes over time

![containers](https://tinyurl.com/mr2ymn54)

**Example:** The container of a banking application

#### MAIN COMPONENTS

- A main component is a software module that is part of a system (classes, routes,
  MVC controllers)
- It represents only the most important parts of the system, not all of them
- It changes quite often

![main-components](https://tinyurl.com/y9ee96v7)

**Example:** The main components of a banking application

#### CODE

- Code is the implementation of the main components
- Permanently chnaging

**Example:** Cart Repository → Cart Model → Cart Controller → Cart View
(Component button, Component discount, etc.)

### ARCHITECTURAL DRIVERS

The influencers of your architecture

#### BUSINESS GOALS

- The most important because is why the problem/opportunity exists in the first
  place
- **Example:** Increase revenue, reduce costs, improve customer experience, etc.

#### TECH TRENDS

- The latest trends in the industry
- Be careful with new born technologies

#### QUALITY ATTRIBUTES

- Or architectural characteristics
- **Example:** Scalability, Performance, Security, Maintainability, etc.
- There's always a baseline for all of these characteristics, the point is to
  highlight the 2/3 more important ones

#### CONSTRAINTS

They are not negotiable, otherwise they are not constraints 😄

**Example:**

- Tech constraints: Use a particular language or framework, etc.
- Business constraints: Stay below a certain budget or meet a deadline, etc.

#### FUNCTIONAL REQUIREMENTS

- The features of your application
- Not all of these are necessarily functional requirements, part of your job is
  to figure out which ones are
- **Example:** User can log in, can create a new account, etc.

#### TEAM'S EXPERIENCE AND KNOWLEDGE

What the team members know, influence a lot

### ARCHITECTURE REQUIREMENTS

- This document is a checklist with the success criteria of your architecture.
  This requeirements come from the **Architectural drivers**.
- [Template in Notion](https://tinyurl.com/2v4873kv)

### ARCHITECTURAL DECISIONS

At the beginning of a project most of the decisions are "Architectural" and
not "Design" because there is no code yet.

**Examples:**

- Deciding the framework to use (some frameworks have a defined structure)
- Making decisions about version control (Monorepo? Large number of repos?,
  etc.)
- Decide how to keep the codebase organised (DDD, clean architecture, etc.)
- Making decisions about using third-party vendors (like Stripe, etc.)
- Making decisions about observability and monitoring (like Prometheus, etc.)

**Don't try to make every decision:**

- 🙁 It probably bocks the entire development process
- 🙁 Taking to much time leading to "analysis paralysis"
- 🚀 Last reponsible moment principle: Only make decisions once we know we have
  as much information as possible

**"Why" is more important than "What":**

- 🚀 Use ADR (Architectural Decision Records) to keep track of decisions
- [Template in Github](https://tinyurl.com/yfw95vxd)

## DESIGNING

### ENTITIES, MODULES, COMPONENTS

#### ENTITIES

It's an abstract concept in our heads, but have meaning in our application

**Example:** Restaurant entity:

Usually gets information from an API (fetch), parses data, has some custom
operations:

- Model → RestaurantModel
- Class/Interface/Type → Restaurant
- Service → useRestaurant()

#### MODULES

- Modules are the bulding blocks of our application.The first level of breakdown
  is going to be "Modules". They are also abstract.
- Sometimes the relation between "Entities" and "Modules" is 1:1, but not always
- Usually represented as a folder, route or page in our application, depending
  on the framework

#### COMPONENTS

Typically see them in code as a view (MVC) or a UI component (React, Vue, etc.)

### DOMAIN MODELING

Method for discovering entities adn describing their attributes and operations:

Used for:

- Data engineering → Define database schemas
- OOP → Define Classes, Interfaces and Hierarchy
- **In Frontend development** → Organise structure and align with UI

When we read functional requirements, there are a lot of nouns repeated Usually
(customer, restaurant, bouquet, etc.) and a lot of verbs associated to these nouns:

- Nouns → Entities
- Verbs → Actions that entities can take

**Example:**

- Entities:
  - Customer
  - Restaurant
  - RestaurantCategory
- Attributes and Operations:
  - Customer:
    - Id: string
    - Name: string
    - Email: string
    - addToFavorites(restaurantId: string): void → _Action it can take_
  - Restaurant:
    - Id: string
    - Name: string
    - Description: string
    - LogoURL: string
    - Address: string
    - searchMenuItems(string): MenuItem[] → _Action it can take_

**Why do this instead of check the API and get the data out of that?**

1.  Naming things accordingly and agreed with the team.

    **Example:**

            ✅ Restaurant | RestaurantCategory | RestaurantLocation | getRestaurantInfo()
            ❌ Restaurant | RestaurantCategory | StoreLocation | getShopInfo()
                        \   /                          |               |
                         \ /                           |               |
                          |                            |               |
                     developer 1                   developer 2     developer 3

2.  Aligning data model to the UI

    **Example:**

            API Response:
            {
                  field1: {
                        **field2: value
                        field3: value
                        field4: {
                              **field5: value
                              field6: value
                        }
                  }
                  **field7: value
                  field8: value
            }

    \*\* fields → These are the fields that makes sense with the UI

    **Align:** Encapsulate the transformation and pass it to the UI

            {
                  data: {
                        field2: value
                        field5: value
                        field7: value
                  }
            }

3.  Establish responsibility

    Have conversations with the team to agreed respoonsibilities

    **Example:**

            ✅ user.addToCart(item)
            or
            ❌ item.addToCart(user) \
            or                       > Because users can have multiple carts, one for each restaurant they are adding items from
            ❌ cart.addItem(item)   /

    Do this exercise at the beginning is a lot cheaper than doing it after once the code is already implemented and therefore more difficult to change

### BREAKING THINGS DOWN

- It refers to the third "C" of the C4 model, meaning the "Components".
- In Frontend architecture we call this "Modules" because "Components" are
  referred to UI components like React components, Vue components, etc.
- Modules are the top level concerns of our application. We can also consider
  them as Mini applications or problems within our application

**Finding modules:**

- We are going to look at the routes or possible routes (we can guess our routes
  by looking at the UI design. Don't have to be 100% accurate)
- Modules don't necessarily map 1to1 entity, not all modules are entities and
  not all entities are modules

**Example:**
| Routes | Module |
| ------ | ------ |
| / | Home |
| /login | Login |
| /delivery | Delivery |
| /pickup | Pickup |
| /restaurant/:id | Restaurant |
| /profile | Profile |
| /search | Search |
| /restaurant/:id/item/:id | MenuItem |

⚠️ "MenuItem" breaks the rule because it is under "Restaurant"

⚠️ "ShoppingCart" does not belong to a route, but it's a module because it is
something that shows up in every page

**Organisation:**

      +----------------+     +----------------+     +----------------+
      |      Home      |     |   Restaurant   |     |    MenuItem    |    ....
      +----------------+     +----------------+     +----------------+
      |      Team 1    |     |      Team 2    |     |       ...      |
      |       or       |     |       or       |     |                |
      |   Developer 1  |     |   Developer 2  |     |                |
      +----------------+     +----------------+     +----------------+

      But there's always going to be dependencies between modules and or shared functionalities


             +------------------------+
             |  Shared functionality  |
             +------------------------+
                         /\
                        /  \
                       /    \
                      /      \
      +----------------+     +----------------+    dependency    +----------------+
      |      Home      |     |   Restaurant   |----------------->|    MenuItem    |    ....
      +----------------+     +----------------+                  +----------------+
      |      Team 1    |     |      Team 2    |                  |       ...      |
      |       or       |     |       or       |                  |                |
      |   Developer 1  |     |   Developer 2  |                  |                |
      +----------------+     +----------------+                  +----------------+

### THE DESIGN DOCUMENTATION

Describe our solution to a problem in some level of detail, and we can share
those documents with different stakeholders or our team and get feeback on the
given solution.

#### STRUCTURE

1. **Overview:** 1 or 2 paragraphs describing what the document is about
2. **context:** Every context that is necessary to understand the document (ex.
   system context diagrams, user stories, etc.)
3. **Goals and Non Goals:** What things are in and out of scope for this problem
4. **High level design:** Describe architecture using 4 dimensions (container
   diagram)
5. **Alternatives considered:** Any framework, libraries or technologies you
   decided not to go with and explain why
6. **Detailed design:** Only in low level design documents. Pseudocode or low
   level diagrams, etc.
7. **Timeline:** How long it will take to implement the solution
8. **Risks & open questions:** Risks and questions that need to be answered
9. **Appendix:** Link to documents

**Example:**

- High level design → Share architecture or something that requires more context
- Low level design → How to implement a particular feature. You can include
  pseudocode, Mock API or Mock data types, etc.

## IMPLEMENTING

### IMPLEMETING MODULES

Common structure:

- 📁 apps

  - 📁 core-api → _Mock API_
  - 📁 docs → _For internal documentation, storybook, etc._
  - 📁 web → _Main NextJS application_
    - 📁 app → _The routing_
      - 📁 delivery
        - 📄 page.tsx → _DeliveryPage()_
      - 📄 layout.tsx
      - 📄 page.tsx → _HomePage()_
    - 📁 common
    - 📁 modules → _Main building blocks of our application_
      - 📁 delivery
      - 📁 home
      - 📁 login
      - 📁 menu-item
      - 📁 pick-up
      - 📁 profile
      - 📁 search
      - 📁 shopping-cart
    - 📁 public
  - 📁 packages (Main NextJS application)

  We put modules separated from app to be able to see all main building blocks
  "at a glance" instead of mixed inside the app folder and subfolders because
  there isn't 1to1 relation between modules and routes

  ### COMPONENTS HIERARCHY & BREACKDOWN

  **Example:**

      +------------------------------------------------+==> FilterableProductTable
      | +--------------------------------------------+=|==> SearchBar
      | | +--------------------+ +----+              | |
      | | | Search...          | | 🔎 |              | |
      | | +--------------------+ +----+              | |
      | |  □ Only products in stock                  | |
      | +--------------------------------------------+ |
      |                                                |
      | +--------------------------------------------+=|==> ProductTable
      | |  Name                              Price   | |
      | | +----------------------------------------+-|=|==> ProductCategoryRow
      | | |                 Fruits                 | | |
      | | +----------------------------------------+ | |
      | | +----------------------------------------+-|=|==> ProductRow
      | | | Apple                              $1  | | |
      | | +----------------------------------------+ | |
      | | +----------------------------------------+-|=|==> ProductRow
      | | | Orange                             $1  | | |
      | | +----------------------------------------+ | |
      | | +----------------------------------------+-|=|==> ProductCategoryRow
      | | |              Vegetables                | | |
      | | +----------------------------------------+ | |
      | | +----------------------------------------+-|=|==> ProductRow
      | | | Spinach                            $2  | | |
      | | +----------------------------------------+ | |
      | | +----------------------------------------+-|=|==> ProductRow
      | | | Pumpkin                            $4  | | |
      | | +----------------------------------------+ | |
      | +--------------------------------------------+ |
      +------------------------------------------------+

#### SCREENS

One of our main entry points of our Modules

#### FEATURES

A "big component" that needs its own internal structure like its own set of folders (components, etc.)

#### COMPONENTS

Smaller components (buttons, inputs, dropdowns, etc.) that are used by other components. Also, they can have smaller sub-components (a dropdown can have a button inside of it).

#### SHARED

- Layouts
- Design System
- Common features
- Shared components
- Utilities

**Example:**

                  +-----------------+    +-----------------+
                  |      Shared     |    |    Module 1     |
                  +-----------------+    +-----------------+
                                                 /\
                                                /  \
                                               /    \
                             +-----------------+    +-----------------+
                             |     Screen 1    |    |    Screen 2     |
                             +-----------------+    +-----------------+
                                     /\
                                    /  \
                                   /    \
                 +-----------------+    +-----------------+
                 |    Feature 1    |    |    Feature 2    |
                 +-----------------+    +-----------------+
                          /\
                         /  \
                        /    \
      +-----------------+    +-----------------+
      |   Component 1   |    |   Component 2   |
      +-----------------+    +-----------------+

A lot of Modules have only 1 screen

### IMPLEMENTING ENTITIES

- Entities are the main building blocks of our domain
- They show up in the entire system, not just in our user interface but also in
  our databases, databases tables, API endpoints, etc.

Normally we have a fetch function to grab our data:

```js
export async function fetchRestaurant(
  restaurantId: string
): Promise<RestaurantResponse> {
  const response = await fetch(`/api/restaurants/${restaurantId}`);
  return response.json();
}
```

This is probably fine with a simple amount of data.

In case of Entities, is better to have a layer of abstraction on top of it
because we can have a response from the API which is not really helpful for the
frontend, for example:

```typescript
data: {
  id: string;
  attributes: {
    name: string;
    description: string;
    image: string;
  };
  relationships: {
    menu: {
      data: {
        id: string;
        type: string;
      };
    };
    reviews: {
      data: [
        {
          id: string;
          type: string;
        },
      ];
    };
  };
}
```

As a frontend, we don't care about "attributes" and "relationships" difference
in terms of nesting the JSON response. Or we don't need all the information. To
solve this, we create a Model:

- Define a Type
- Create a Class or function aggregating all the data (also from different data
  sources if needed) we need

```typescript
// Define the type to reflect the API's complex response structure
type ApiResponse = {
  data: {
    id: string;
    attributes: {
      name: string;
      description: string;
      image: string;
    };
    relationships: {
      menu: {
        data: {
          id: string;
          type: string;
        };
      };
      reviews: {
        data: Array<{
          id: string;
          type: string;
        }>;
      };
    };
  };
};
```

```typescript
// Simplified model for the frontend
type MenuItem = {
  id: string;
  name: string;
  description: string;
  imageUrl: string;
  menuId: string;
  reviewIds: string[];
};
```

```typescript
class MenuItemModel implements MenuItem {
  id: string;
  name: string;
  description: string;
  imageUrl: string;
  menuId: string;
  reviewIds: string[];

  constructor(apiResponse: ApiResponse) {
    const { id, attributes, relationships } = apiResponse.data;

    this.id = id;
    this.name = attributes.name;
    this.description = attributes.description;
    this.imageUrl = attributes.image;
    this.menuId = relationships.menu.data.id;
    this.reviewIds = relationships.reviews.data.map((review) => review.id);
  }
}
```

```typescript
const apiResponse: ApiResponse = {
  data: {
    id: "123",
    attributes: {
      name: "Burger",
      description: "Delicious veggie burger",
      image: "/images/burger.png",
    },
    relationships: {
      menu: {
        data: {
          id: "menu-456",
          type: "menu",
        },
      },
      reviews: {
        data: [
          { id: "review-789", type: "review" },
          { id: "review-101", type: "review" },
        ],
      },
    },
  },
};

const menuItem = new MenuItemModel(apiResponse);
console.log(menuItem);
```

### GUARDRAILS AND CONSTRAINTS

#### DEPENDENCY CRUISER

A tool to validate the dependencies of our code base against a set of rules

**Example:**

Rule: Modules should not depend on each other

                                                  +-----------------+
                                                  |     Modules     |\
                                                  +-----------------+ \
                                                 /\                    \
                                                /  \                    \
                                               /    \                    \
                             +-----------------+    +----------- ------+  \+-----------------+
                             |    Restaurant   |    |    Delivery     |    |      Search     |
                             +-----------------+    +-----------------+    +-----------------+
                                     /\                                             /\
                                    /  \                                           /  \
                                   /    \                                         /    \
                 +-----------------+    +-----------------+     +-----------------+    +-----------------+
                 |    Feature 1    |    |    Feature 2    |     |    Feature 3    |    |    Feature 4    |
                 +-----------------+    +-----------------+     +-----------------+    +-----------------+
                          /\                                            /\                      \
                         /  \                                          /  \                      \
                        /    \                                        /    \                      \
      +-----------------+    +-----------------+    +-----------------+    +-----------------+    +-----------------+
      | ✅ Component 1  |    | ✅ Component 2  |    | ✅ Component 3  |    | ✅ Component 4  |    | ❌ Component 2  |
      +-----------------+    +-----------------+    +-----------------+    +-----------------+    +-----------------+

Feature 4 needs to use Component 2, but it's not allowed because Component 2
belongs to Module Restaurant and Feature 4 belongs to Module Search

Dependecy cruiser will look for this kind of rules previously defined and will
break the build if it finds a violation

#### COMMONALITY

Used mostly in Monorepos. Check for things like circular dependencies. You can
also define ownership of certain packages, tag them, etc.

#### BUNDLESIZE

Simple check of our bundles. You can set limits that, if they are exceeded,
will break the build

#### PERFORMANCE BUDGET

Define thresholds for different sort of web metrics like: FPS, TTI, FCP, LCP,
etc. (Ex. Speedcurve)

#### SONARLINT

To help managing the complexity of our code base (cognitive complexity like too
many execution paths, functions too long, etc.)
