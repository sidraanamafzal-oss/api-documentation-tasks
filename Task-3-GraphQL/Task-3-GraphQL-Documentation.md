
Task 3: GraphQL API Documentation
1. Introduction
GraphQL is a query language and API technology that allows clients to request exactly the data they need from a server. Unlike traditional REST APIs, where the server usually determines the structure of the response, GraphQL allows the client to specify the required fields.
This documentation explores a GraphQL endpoint using introspection and demonstrates simple queries, complex nested queries, avoiding over-fetching, mutations, and the use of AI to convert a REST API requirement into an optimized GraphQL query.
________________________________________
2. Exploring the GraphQL Endpoint Using Introspection
GraphQL provides a special introspection system that allows developers to examine the available schema, queries, fields, and other information.
The following introspection query was used:
query {
  __schema {
    queryType {
      fields {
        name
        description
      }
    }
    mutationType {
      fields {
        name
        description
      }
    }
  }
}
The result showed that the endpoint provides the following query fields:
•	continent
•	continents
•	countries
•	country
•	language
•	languages
The introspection result also showed that mutationType was null. Therefore, the selected endpoint does not provide mutation operations.
 
________________________________________
3. Constructing a Basic GraphQL Query
After exploring the schema, a basic query was created to retrieve country information.
query {
  countries {
    code
    name
  }
}
This query requests the country code and country name.
The advantage of GraphQL is that the developer specifies exactly which fields are required instead of receiving the complete object.
 
________________________________________
4. Constructing a Complex/Nested Query
GraphQL also allows developers to retrieve related information using nested selections.
The following query was tested successfully:
query {
  countries {
    code
    name
    capital
    currency
    continent {
      code
      name
    }
  }
}
This is a complex/nested query because the continent field contains additional fields such as code and name.
The response provides country information together with related continent information in the same query structure.
The nested structure can make it easier for an application to request related data according to its requirements.
 
________________________________________
5. Avoiding Over-Fetching
Over-fetching occurs when an application receives more data than it actually needs.
For example, suppose a website only needs the country name and capital. Instead of requesting many fields, GraphQL allows the developer to request only those two fields.
query {
  countries {
    name
    capital
  }
}
The response contains only the requested fields.
This demonstrates one of the important benefits of GraphQL: the client can select the fields it needs. Unnecessary fields such as currency or country code are not included in the query.
Therefore, GraphQL provides a more targeted way of requesting data and can help reduce unnecessary data retrieval.
 
________________________________________
6. GraphQL Mutations
A GraphQL mutation is used to modify data. Common operations include:
•	Creating data
•	Updating data
•	Deleting data
For example, a mutation-enabled GraphQL API could have a mutation such as:
mutation {
  createUser(
    name: "Ali"
    email: "ali@example.com"
  ) {
    id
    name
    email
  }
}
This example creates a user and requests the user's ID, name, and email in the response.
Mutation Support in the Selected Endpoint
During introspection, the selected country GraphQL endpoint returned:
mutationType: null
This indicates that this particular endpoint does not expose mutation operations. Therefore, a mutation could not be executed on this endpoint.
The mutation example above is provided only to explain the structure and purpose of GraphQL mutations.
________________________________________
7. AI-Assisted REST-to-GraphQL Conversion
AI can help developers translate application requirements into GraphQL query structures.
REST API Requirement
The requirement is:
A website needs to display the country name, capital, and continent name for every country. It does not need currency, country code, or other fields.
AI Prompt
The following prompt was given to AI:
I have a REST API requirement:

A website needs to display the country name, capital, and continent name for every country. It does not need currency, country code, or other fields.

Convert this requirement into an optimized GraphQL query. The query should retrieve only the required fields and should avoid over-fetching. Explain why the query is optimized.
AI-Generated GraphQL Structure
query {
  countries {
    name
    capital
    continent {
      name
    }
  }
}
Explanation
The query requests only the information required by the website:
•	Country name
•	Capital
•	Continent name
It does not request unnecessary fields such as currency or country code.
The nested continent { name } structure allows the required continent name to be retrieved together with each country.
This demonstrates how AI can assist developers in translating a data requirement into a targeted GraphQL query while considering the problem of over-fetching.
 
8. Benefits of GraphQL
The exploration demonstrates several useful characteristics of GraphQL:
1. Flexible data selection
Clients can request specific fields instead of receiving an entire object.
2. Nested data
Related data can be requested using nested selections within a query.
3. Reduced over-fetching
Applications can avoid requesting fields that they do not need.
4. Introspection
Developers can inspect the GraphQL schema and discover available operations and fields.
5. AI-assisted development
AI can help translate application requirements into GraphQL query structures and identify unnecessary fields.
________________________________________
9. Conclusion
GraphQL provides a flexible way for developers to request data from an API. Through introspection, developers can explore the available schema and understand which queries and fields are supported.
The practical exploration demonstrated basic and complex nested queries and showed how selecting only required fields can help avoid over-fetching. The selected endpoint did not support mutations, as indicated by mutationType: null.
The AI-assisted REST-to-GraphQL example also demonstrated how AI can help developers transform a data requirement into a focused GraphQL query. Overall, GraphQL provides developers with greater control over the structure of the data they request.
