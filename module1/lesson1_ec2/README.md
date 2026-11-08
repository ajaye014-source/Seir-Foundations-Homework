# Class 8 / SEIR Foundations: HW Submission Repo


# Tech & Banking Foundations: How Enterprise Systems Talk to Each Other

## 1. Databases: The System’s Filing Cabinet

A **database** is simply a digital filing system built to store, organize, and retrieve information quickly. Instead of picking a tool just because it is popular, organizations pick a database based on the specific job it needs to perform.

```
+-----------------------------------------------------------------------+
|                           DATABASE CHOICE                             |
+-----------------------------------+-----------------------------------+
|       Relational (SQL)            |       Non-Relational (NoSQL)      |
|  Strict tables, rows, & columns   | Flexible documents & key-value    |
|   Great for structured transactions   | Great for rapidly changing data   |
+-----------------------------------+-----------------------------------+

```

* **Relational Databases (SQL):** Store data in neat tables with rows and columns (like a giant, interconnected spreadsheet). They enforce strict rules so data stays accurate—making them ideal for bank accounts and order histories. **PostgreSQL** is often the default choice in the industry because it handles complex calculations reliably and is open-source. However, it can struggle to handle massive bursts of unorganized data without extra setup.
* **Non-Relational Databases (NoSQL):** Store data flexibly without rigid spreadsheets—using loose documents, key pairs, or charts instead. They excel at handling fast-changing, unstructured data like social media feeds or live product catalogs.
* **How to Pick One:** Ask key questions upfront: *Is the data neat or messy? Do we need strict rules or room to grow? How fast does it need to respond?* Choosing the wrong setup leads to slow load times, data crashes, or system failures down the road.

---

## 2. COBOL: The Engine Behind Old Mainframes

**COBOL** (Common Business-Oriented Language) is a programming language built back in 1959 by a government and industry group (CODASYL) backed by the U.S. Department of Defense. It was written so that business logic could look closer to plain English than raw machine code.

* **Where It Lives:** It runs on heavy-duty enterprise computers called mainframes. It handles massive, repetitive math calculations—like batching overnight bank balances, insurance payouts, and government payrolls.
* **Why It’s Still Around:** Over **800 billion lines of COBOL code** are estimated to still be active globally. Replacing it is risky and expensive because these systems process trillions of dollars daily without breaking down.
* **The Talent Challenge:** The average COBOL developer is approaching retirement age, leaving a shrinking pool of engineers who know how to maintain these systems. Replacing a COBOL core takes years of work and millions of dollars, so companies often preserve the old code rather than rebuilding it from scratch.

---

## 3. SWIFT: The Postal Service for Global Banks

**SWIFT** (Society for Worldwide Interbank Financial Telecommunication) was launched in 1977 by a coalition of international banks to replace noisy, unreliable telex wires.

> **Key Rule:** SWIFT does **not** move money. It sends the secure, standardized text messages that tell banks *how* and *when* to move the money internally.

* **Competition & Usage:** SWIFT connects over 11,000 financial institutions worldwide. Alternatives like CIPS (China) or SFPS (Russia) exist, but SWIFT remains the global standard.
* **The Upgrade (ISO 20022):** The financial world has moved away from old, limited text formats (like **MT103** for single transfers or **MT202** for bank-to-bank settlements) to a rich XML/data format called **ISO 20022** (using standard messages like **pacs.008** and **pacs.009**).
* **The Coexistence Window:** The official transition period for cross-border payment instructions concluded on **November 22, 2025**. While financial institutions can no longer use legacy MT formats for cross-border payments without incurring network conversion fees, the broader transition to fully structured addresses and exceptions will continue unfolding through 2026 and 2027.

---

## 4. APIs: The Digital Receptionist

An **API** (Application Programming Interface) is a set of rules that allows two separate applications to talk to one another. Think of an API like a waiter in a restaurant: you look at the menu, tell the waiter your order (the request), the waiter takes it to the kitchen (the system), and returns with your food (the data).

```
[ User / App ]  ===( Request: GET/POST )===>  [ API Interface ]  ===>  [ Mainframe / DB ]
[ User / App ]  <===( Response: JSON )======  [ API Interface ]  <===  [ Mainframe / DB ]

```

* **How It Works:** Modern web connections use **HTTP** (the backbone of the web). **REST APIs** use lightweight text formats like **JSON** to deliver information.
* **GET Requests:** Ask to read data (e.g., "Show me my balance").
* **POST Requests:** Ask to submit new data (e.g., "Transfer $50").


* **Security & AI:** Roughly 82% of enterprises rely on APIs for mobile apps, payment gateways, and connecting AI models to company data. Because APIs expose data to the outside world, they must **validate incoming data**—checking every request to prevent hacker attacks or corrupted records from reaching internal servers.

---

## 5. Putting It All Together: Bringing Old Systems into the Future

When a modern mobile app sends money internationally, all four technologies work together in a single chain:

```
+------------------------------------------------------------------------------------+
| 1. Modern Entry    | User taps "Send Money" on an app; request goes to a modern    |
|    (API / Python)  | FastAPI wrapper using HTTP and JSON.                          |
+--------------------+---------------------------------------------------------------+
| 2. Standard Message| The system translates the request into an ISO 20022 (SWIFT)   |
|    (SWIFT / XML)   | pacs.008 format so international banks agree on the terms.    |
+--------------------+---------------------------------------------------------------+
| 3. Business Logic  | The API passes data to an underlying COBOL program on a       |
|    (COBOL / Files) | mainframe using fixed-width layout files to check account rules|
|                    | and calculate fees.                                           |
+--------------------+---------------------------------------------------------------+
| 4. Data Storage    | Transaction history is written to a relational database       |
|    (Database / SQL)| (like PostgreSQL or SQLite) for auditing and record-keeping.   |
+------------------------------------------------------------------------------------+

```

### Why Government & Enterprise Systems Wrap Old Code in APIs

Reports from the U.S. Government Accountability Office (GAO) highlight that major government agencies, healthcare networks, and banks still rely on decades-old mainframes. Fully rewriting millions of lines of proven COBOL logic carries high risk and massive expense.

Instead of ripping out the old core, organizations build **API wrappers**. The API sits in front of the legacy COBOL system like a translator—allowing modern web pages, mobile apps, and AI assistants to communicate with 50-year-old code safely and efficiently.


