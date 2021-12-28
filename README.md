Tutorial - User Guide
1. Install FastAPI
    pip install "fastapi[all]"

    # Want to deploy your app to production
    pip install fastapi

    # install uvicorn to work as the server
    pip install "uvicorn[standard]"

2. Run the live server
    uvicorn main:app --reload
    
    # The command uvicorn main:app refers to:
    main: the file main.py (the Python "module").
    app: the object created inside of main.py with the line app = FastAPI().
    --reload: make the server restart after code changes. Only use for development.

3. Check it
    Open your browser at http://127.0.0.1:8000

4. Interactive API docs
    Now go to http://127.0.0.1:8000/docs
    You will see the automatic interactive API documentation (provided by Swagger UI)

5. Alternative API docs
    And now, go to http://127.0.0.1:8000/redoc.
    You will see the alternative automatic documentation (provided by ReDoc)

6. Query Parameters
    When you declare other function parameters that are not part of the path parameters, they are automatically interpreted as "query" parameters.

7. Request Body
    + When you need to send data from a client (let's say, a browser) to your API, you send it as a request body.
    + A request body is data sent by the client to your API. A response body is the data your API sends to the client.

8. Singular values in body
    The same way there is a Query and Path => FastAPI provides an equivalent Body.

9. Body - Fields
    + The same way you can declare additional validation and metadata in path operation function parameters with Query, Path and Body => Field.
    + Notice that Field is imported directly from pydantic, not from fastapi as are all the rest (Query, Path, Body, etc).

10. Extra Data Types
    + UUID:
    - A standard "Universally Unique Identifier", common as an ID in many databases and systems.
    - In requests and responses will be represented as a str.
    + datetime.datetime:
    - A Python datetime.datetime.
    - In requests and responses will be represented as a str in ISO 8601 format, like: 2008-09-15T15:53:00+05:00.
    + datetime.date:
    - Python datetime.date.
    - In requests and responses will be represented as a str in ISO 8601 format, like: 2008-09-15.
    + datetime.time:
    - A Python datetime.time.
    - In requests and responses will be represented as a str in ISO 8601 format, like: 14:23:55.003.
    + datetime.timedelta:
    - A Python datetime.timedelta.
    - In requests and responses will be represented as a float of total seconds.
    - Pydantic also allows representing it as a "ISO 8601 time diff encoding"
    + frozenset:
    - In requests and responses, treated the same as a set:
        . In requests, a list will be read, eliminating duplicates and converting it to a set.
        . In responses, the set will be converted to a list.. The generated schema will specify that the set values are unique (using JSON Schema's uniqueItems).
    + bytes:
    - Standard Python bytes.
    - In requests and responses will be treated as str.
    - The generated schema will specify that it's a str with binary "format".
    + Decimal:
    - Standard Python Decimal.
    - In requests and responses, handled the same as a float.

11. Cookie Parameters
    + You can define Cookie parameters the same way you define Query and Path parameters
    + Declare Cookie parameters: The first value is the default value, you can pass all the extra validation or annotation parameters

12. Response Model
    + You can declare the model used for the response with the parameter response_model in any of the path operations:
    @app.get()
    @app.post()
    @app.put()
    @app.delete()
    + Notice that response_model is a parameter of the "decorator" method (get, post, etc). Not of your path operation function, like all the parameters and body.