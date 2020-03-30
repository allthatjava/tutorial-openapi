OpenAPI v2.0 and v3.0 example

### Minimum required structure
* v2.0
```yaml
swagger: "2.0"            # Required
info:                     # Required
  version: "1.0"          # Required
  title: "Sample of Swagger(OpenAPI) 2.0"   # Required
paths:                    # Required
  /:
    get:
      responses:          # Required by 'get'
        200:
          description: index page           # Required by 'responses'
```
* v3.0
```yaml
openapi: 3.0.3            # Required
info:                     # Required
  version: '1.0'          # Required
  title: Sample of Swagger(OpenAPI) 3.0   # Required
paths:                    # Required
  /:
    get:
      responses:          # Required by 'get'
        200:
          description: index page           # Required by 'responses'
```

### Add Response inline
##### Primitive type
* v2.0
```yaml
paths:                    # Required
  /customers:
    get:
      produces:
        - application/json                        # Resposne content type
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          schema:
            type: array
            items:
              type: string
              description: Customer Name
              minLength: 3                        # Optional
              maxLength: 100                      # Optional
```
* v3.0
```yaml
paths:                    # Required
  /customers:
    get:
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          content:
            application/json:                 # Resposne content type
              schema:                         # Content's type
                type: array                   # Array(List) of the following items
                items:                        # If above type is 'array', 'items' must be present
                  type: string
                  description: Customer Name
                  minLength: 3                # Optional
                  maxLength: 100              # Optional
```

##### Object
* v2.0
```yaml
paths:                    # Required
  /customers:
    get:
      produces:
        - application/json                        # Resposne content type
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          schema:                         # Content's type
            type: array                   # Array(List) of the following items
            items:                        # If above type is 'array', 'items' must be present
              type: object
              description: Customer
              properties:
                fullName:
                  type: string
                  minLength: 2
                  maxLength: 100
                  example: John Smith
                age:
                  type: integer
                  example: 40
                height:
                  description: Height in Feet format
                  type: number
                  format: float             # Optional for detail format
                  example: 6.1
                address:
                  type: object
                  description: Address
                  properties:
                    street1:
                      type: string
                      example: 123 abc st.
                    street2:
                      type: string
                      example: unit 20
                    provinceCode:
                      type: string
                      minLength: 2
                      maxLength: 2
                      enum:
                        - 'ON'          # Without quotation it will display 'true' instead on 'ON'.
                        - QC
                        - BC
                    postalCode:
                      type: integer
                      maxLength: 5
                      example: 12345
```
* v3.0
```yaml
paths:                    # Required
  /customers:
    get:
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          content:
            application/json:                 # Resposne content type
              schema:                         # Content's type
                type: array                   # Array(List) of the following items
                items:                        # If above type is 'array', 'items' must be present
                  type: object
                  description: Customer
                  properties:
                    fullName:
                      type: string
                      minLength: 2
                      maxLength: 100
                      example: John Smith
                    age:
                      type: integer
                      example: 40
                    height:
                      description: Height in Feet format
                      type: number
                      format: float             # Optional for detail format
                      example: 6.1
                    address:
                      type: object
                      description: Address
                      properties:
                        street1:
                          type: string
                          example: 123 abc st.
                        street2:
                          type: string
                          example: unit 20
                        provinceCode:
                          type: string
                          minLength: 2
                          maxLength: 2
                          enum:
                            - 'ON'          # Without quotation it will display 'true' instead on 'ON'.
                            - QC
                            - BC
                        postalCode:
                          type: integer
                          maxLength: 5
                          example: 12345
```

### Add Response with References
* v2.0
```yaml
paths:                    # Required
  /customers:
    get:
      produces:
        - application/json                        # Resposne content type
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          schema:                         # Content's type
            $ref: '#/definitions/CustomerList'
definitions:
  Address:
    type: object
    description: Address
    properties:
      street1:
        type: string
        example: 123 abc st.
      street2:
        type: string
        example: unit 20
      provinceCode:
        type: string
        minLength: 2
        maxLength: 2
        enum:
          - 'ON'          # Without quotation it will display 'true' instead on 'ON'.
          - QC
          - BC
      postalCode:
        type: integer
        maxLength: 5
        example: 12345
  Customer:
    type: object
    description: Customer
    properties:
      fullName:
        type: string
        minLength: 2
        maxLength: 100
        example: John Smith
      age:
        type: integer
        example: 40
      height:
        description: Height in Feet format
        type: number
        format: float             # Optional for detail format
        example: 6.1
      address:
        $ref: '#/definitions/Address'
  CustomerList:
    type: array                   # Array(List) of the following items
    items:                        # If above type is 'array', 'items' must be present
      $ref: '#/definitions/Customer'
```
* v3.0
```yaml
paths:                    # Required
  /customers:
    get:
      responses:          # Required by 'get'
        200:
          description: List of Customer           # Required by 'responses'
          content:
            application/json:                 # Resposne content type
              schema:                         # Content's type
                $ref: '#/components/schemas/CustomerList'
components:
  schemas:
    Address:
      type: object
      description: Address
      properties:
        street1:
          type: string
          example: 123 abc st.
        street2:
          type: string
          example: unit 20
        provinceCode:
          type: string
          minLength: 2
          maxLength: 2
          enum:
            - 'ON'          # Without quotation it will display 'true' instead on 'ON'.
            - QC
            - BC
        postalCode:
          type: integer
          maxLength: 5
          example: 12345
    Customer:
      type: object
      description: Customer
      properties:
        fullName:
          type: string
          minLength: 2
          maxLength: 100
          example: John Smith
        age:
          type: integer
          example: 40
        height:
          description: Height in Feet format
          type: number
          format: float             # Optional for detail format
          example: 6.1
        address:
          $ref: '#/components/schemas/Address'
    CustomerList:
      type: array                   # Array(List) of the following items
      items:                        # If above type is 'array', 'items' must be present
        $ref: '#/components/schemas/Customer'
```

### Inheritance
The keyword 'allOf' let the children node(Sports,Truck) refer the parent node (Car)

* v2.0
```yaml
definitions:
  Car:
    type: object
    properties:
      drivable:
        type: boolean
  Sports:
    type: object
    allOf:
      - $ref: '#/definitions/Car'
    properties:
      engineLocation:
        type: string
        enum:
          - FRONT
          - REAR
  Truck:
    type: object
    allOf:
      - $ref: '#/definitions/Car'/Car'
    properties:
      flatbedSize:
        description: Square Feet
        type: integer
        example: 30
```

* v3.0 
```yaml
components:
    Car:
      type: object
      properties:
        drivable:
          type: boolean
    Sports:
      type: object
      allOf:
        - $ref: '#/components/schemas/Car'
      properties:
        engineLocation:
          type: string
          enum:
            - FRONT
            - REAR
    Truck:
      type: object
      allOf:
        - $ref: '#/components/schemas/Car'
      properties:
        flatbedSize:
          description: Square Feet
          type: integer
          example: 30
```


### Put operation

* v2.0
```yaml
paths:                    # Required
  /customers:
    put:
      summary: Updates a customer
      description: This will update a **Customers** object
      tags:
        - Customers
      operationId: updateCustomer
      parameters:
        - $ref: '#/parameters/customerIdPathParam'  # path param
        - $ref: '#/parameters/customer'             # request body param
      responses:
        204:
          description: Customer Updated
parameters:
  customer:
    name: customerObj
    in: body
    schema:
      type: object
      $ref: '#/definitions/Customer'
  customerIdPathParam:
    name: customerId
    description: Customer's Id
    in: path
    schema:
      type: string
      format: uuid
definitions:
  Customer:
    type: object
    description: Customer
    properties:
      id:
        type: string
        format: uuid
        readOnly: true
      fullName:
        type: string
        minLength: 2
        maxLength: 100
        example: John Smith
      age:
        type: integer
        example: 40
      height:
        description: Height in Feet format
        type: number
        format: float             # Optional for detail format
        example: 6.1
      address:
        $ref: '#/definitions/Address'
```
* v3.0
```yaml
paths:                    # Required
  /customers:
    put:
      summary: Updates a customer
      description: This will update a **Customers** object
      tags:
        - Customers
      operationId: updateCustomer
      parameters:
        - $ref: '#/components/parameters/customerIdPathParam'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Customer'
      responses:
        204:
          description: Customer Updated
        400:
          description: Bad Request
        409:
          description: Conflict
components:
  parameters:
    customerIdPathParam:
      name: customerId
      description: Customer's Id
      in: path
      schema:
        type: string
        format: uuid
  schemas:
    Customer:
      type: object
      description: Customer
      properties:
        id:
          type: string
          format: uuid
          readOnly: true
        fullName:
          type: string
          minLength: 2
          maxLength: 100
          example: John Smith
        age:
          type: integer
          example: 40
        height:
          description: Height in Feet format
          type: number
          format: float             # Optional for detail format
          example: 6.1
        address:
          $ref: '#/components/schemas/Address'
```

### Delete Operation
* v2.0
```yaml
paths:                    # Required
  /customers/{customerId}:
    delete:
      summary: Deletes a customer
      description: This will delete the given **Customers** object
      tags:
        - Customers
      operationId: deleteCustomer                    # Codegen will use this name as method name
      parameters:
        - $ref: '#/parameters/customerIdPathParam'
      responses:
        200:
          description: Customer deleted
parameters:
  customerIdPathParam:
    name: customerId
    description: Customer's Id
    in: path
    schema:
      type: string
      format: uuid
```
* v3.0
```yaml
paths:                    # Required
  /customers/{customerId}:
    delete:
      summary: Deletes a customer
      description: This will delete the given **Customers** object
      tags:
        - Customers
      operationId: deleteCustomer
      parameters:
        - $ref: '#/components/parameters/customerIdPathParam'
      responses:
        200:
          description: Customer Deleted
        400:
          description: Bad Request
components:
    customerIdPathParam:
      name: customerId
      description: Customer's Id
      in: path
      schema:
        type: string
        format: uuid
```

### Security - Basic
v3.0
```yaml
security:
  - BasicAuth: []
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic
```

### Security - JWT
v3.0
```yaml
security:
  - JwtAuthToken: []
components:
  securitySchemes:
    JwtAuthToken:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

### Security - Anonymous Authentication
v3.0
```yaml
paths:                    # Required
  /customers:
    get:
      ...
      security: []

security:
  - JwtAuthToken: []
components:
  securitySchemes:
    JwtAuthToken:
      type: http
      scheme: bearer
      bearerFormat: JWT
```