# RAG and Dynamic filters *What is this*?. That is what we will understand it *Here*

## What is RAG?

**RAG** *or* **Retrieval-Augmented Generation** is a something that is external from the LLM and we can say it's a **Library** that help the model get up-to date information

## What is Dynamic filters?

**Dynamic filters are temporary, query-specific constraints generated from a user’s input to narrow down a search space before retrieval (e.g., vector search or database search).**

**Explaning:**

*Dynamic filters are rules that the system temporarily creates from your question to decide what data to search*


**Example:**

**user** = What is the strongest millitray in the world?

**What dynamic filters do:**

**Topic** : Millitray
**Comprasion** : Strongest

### But here we can face a problem because when the user ask the agent something like: *Give me the holidays in my company* The agent can give the user a wrong or very sensvtive data

**And the semantic search will do it's job by getting the company holidays but what if the data that have given to the user is talking about holidays but it's was also so *sensitive* like it's the *CEO* file, or what if the data is from *2021* soo it's outdated?**

### Soo here where it comes *Dynamic filters*

**Metadata is a structured extra informaton** Example:

- department: "HR"
- region: "US"
- security_level: "Internal"

- 3. Combining them at "Query Time"
When you apply a filter, you are effectively narrowing the search space before the computer does any heavy math.

Without Filters: The computer calculates the similarity score for all 1,000,000 documents in your database. This is slow and risky.
With Filters: The computer first ignores 99% of the database that doesn't match your criteria (e.g., it tosses out everything that isn't department: "HR"). It then only performs the complex vector math on the remaining relevant documents.


### What is the diffrence between Metadata and dynamic search?

**You can think of it like:**

**Metadata = information written on the box**
**Dynamic filters = It's saying: Just open the thing than written on it *HR***

Soo at the end you can say:

**Metadata : What is this thing: *HR, Date, etc***
**Dynamic filters : just open the relevant things for the topic**
