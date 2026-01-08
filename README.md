# Task 1 - Spring MVC Application

Name:  Sagar Gupta
Student Id: 61740



## Project Description

This is a Spring Boot MVC application created as part of the Spring Framework course at Vistula University. The application demonstrates basic Spring MVC concepts including:
- Creating a Spring Boot project from scratch
- Implementing a Spring Controller
- Using `@ResponseBody` annotation for direct response
- Using Thymeleaf templ


ates for view rendering
- Following the MVC (Model-View-Controller) design pattern
<img width="1470" height="956" alt="Screenshot 2026-01-08 at 14 54 09" src="https://github.com/user-attachments/assets/220bc432-1c6f-4ca1-9ed8-08b8a6a23cee" />



## Technologies Used

- **Java 17**
- **Spring Boot 4.0.1**
- **Spring Web MVC** - For handling HTTP requests and MVC architecture
- **Thymeleaf** - Template engine for server-side rendering
- **Lombok** - For reducing boilerplate code
- **Maven** - Build and dependency management

## Project Structure

```
task1-spring-mvc-61740-Sagar/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── pl/
│   │   │       └── edu/
│   │   │           └── vistula/
│   │   │               ├── task1_spring_mvc/
│   │   │               │   └── Task1SpringMvcApplication.java
│   │   │               └── task1springmvc/
│   │   │                   └── controller/
│   │   │                       └── HelloController.java
│   │   └── resources/
│   │       ├── application.properties
│   │       ├── static/
│   │       │   ├── favicon.png
│   │       │   └── images/
│   │       │       └── vistula.png
│   │       └── templates/
│   │           └── greeting.html
│   └── test/
└── pom.xml
```

## How to Run the Application

### Prerequisites
- Java 17 or higher installed
- Maven installed (or use the included Maven wrapper)

### Running the Application

1. **Using Maven Wrapper (Recommended):**
   ```bash
   ./mvnw spring-boot:run
   ```
   On Windows:
   ```bash
   mvnw.cmd spring-boot:run
   ```

2. **Using Maven (if installed globally):**
   ```bash
   mvn spring-boot:run
   ```

3. **Using IDE:**
   - Open the project in your IDE (IntelliJ IDEA, Eclipse, etc.)
   - Run the `Task1SpringMvcApplication.java` class

The application will start on **http://localhost:8080**

## API Endpoints

### 1. Root Endpoint - GET `/`

**Description:** Returns a plain text greeting message using `@ResponseBody` annotation.

**HTTP Method:** `GET`

**URL:** `http://localhost:8080/`

**Request Parameters:** None

**Response:** 
- **Content-Type:** `text/plain`
- **Body:** `Hello Vistula, in my first Spring controller.`

**Example:**
```
GET http://localhost:8080/
```

**Screenshot:** *[Add screenshot of browser showing "Hello Vistula, in my first Spring controller."]*

**Code Explanation:**
```java
@GetMapping("/")
@ResponseBody
public String hello() {
    return "Hello Vistula, in my first Spring controller.";
}
```
- `@GetMapping("/")` - Maps HTTP GET requests to the root path `/`
- `@ResponseBody` - Tells Spring to return the method's return value directly as the HTTP response body, bypassing view resolution
- The method returns a String which is sent directly to the client as plain text

---

### 2. Greeting Endpoint - GET `/greeting`

**Description:** Returns a Thymeleaf HTML view with a personalized greeting. This demonstrates the MVC pattern where the controller processes the request, adds data to the model, and returns a view name.

**HTTP Method:** `GET`

**URL:** `http://localhost:8080/greeting`

**Request Parameters:**
- `name` (optional) - The name to display in the greeting. Defaults to "World" if not provided.

**Response:**
- **Content-Type:** `text/html`
- **Body:** HTML page with personalized greeting and Vistula logo

**Examples:**

1. **Without parameter (uses default):**
   ```
   GET http://localhost:8080/greeting
   ```
   Result: Displays "Hello World"

2. **With name parameter:**
   ```
   GET http://localhost:8080/greeting?name=Vistula
   ```
   Result: Displays "Hello Vistula"

3. **With custom name:**
   ```
   GET http://localhost:8080/greeting?name=John
   ```
   Result: Displays "Hello John"

**Screenshots:**
- *[Add screenshot of browser showing greeting with default "World"]*
- *[Add screenshot of browser showing greeting with name="Vistula"]*

**Code Explanation:**
```java
@GetMapping("/greeting")
public String greeting(
        @RequestParam(name = "name", defaultValue = "World") String name,
        Model model
) {
    model.addAttribute("name", name);
    return "greeting";
}
```
- `@GetMapping("/greeting")` - Maps HTTP GET requests to `/greeting` path
- `@RequestParam(name = "name", defaultValue = "World")` - Extracts the `name` query parameter from the URL. If not provided, defaults to "World"
- `Model model` - Spring's Model object used to pass data from controller to view
- `model.addAttribute("name", name)` - Adds the name to the model so it can be accessed in the Thymeleaf template
- `return "greeting"` - Returns the view name. Spring will look for `greeting.html` in the `templates` directory

**Thymeleaf Template (`greeting.html`):**
```html
<h1 th:text="'Hello ' + ${name}"></h1>
<img src="/images/vistula.png" width="300"/>
```
- `th:text` - Thymeleaf attribute that sets the text content of the element
- `${name}` - Accesses the "name" attribute from the model
- The image is served from the static resources directory

---

## Use Cases

### Use Case 1: Simple Text Response
**Scenario:** User wants to see a simple greeting message
1. Open browser or use Postman
2. Navigate to `http://localhost:8080/`
3. View the plain text response: "Hello Vistula, in my first Spring controller."

### Use Case 2: Personalized Greeting with Default Name
**Scenario:** User wants to see a greeting page with default name
1. Open browser
2. Navigate to `http://localhost:8080/greeting`
3. View the HTML page displaying "Hello World" with the Vistula logo

### Use Case 3: Personalized Greeting with Custom Name
**Scenario:** User wants to see a greeting with their name
1. Open browser
2. Navigate to `http://localhost:8080/greeting?name=Vistula`
3. View the HTML page displaying "Hello Vistula" with the Vistula logo

### Use Case 4: Testing with Postman
**Scenario:** Developer wants to test endpoints using Postman

1. **Test Root Endpoint:**
   - Method: GET
   - URL: `http://localhost:8080/`
   - Expected Response: Plain text "Hello Vistula, in my first Spring controller."

2. **Test Greeting Endpoint (Default):**
   - Method: GET
   - URL: `http://localhost:8080/greeting`
   - Expected Response: HTML page with "Hello World"

3. **Test Greeting Endpoint (With Parameter):**
   - Method: GET
   - URL: `http://localhost:8080/greeting?name=Vistula`
   - Expected Response: HTML page with "Hello Vistula"

**Screenshots:**
- *[Add Postman screenshot showing GET request to root endpoint]*
- *[Add Postman screenshot showing GET request to /greeting endpoint]*

---

## Key Concepts Demonstrated

### 1. @Controller Annotation
The `@Controller` annotation marks the class as a Spring MVC controller. It's a specialization of `@Component` that indicates the class's role in the MVC pattern.

### 2. @ResponseBody Annotation
The `@ResponseBody` annotation tells Spring to serialize the return value directly into the HTTP response body, bypassing view resolution. This is useful for REST APIs or when returning plain text/JSON.

### 3. @GetMapping Annotation
`@GetMapping` is a composed annotation that acts as a shortcut for `@RequestMapping(method = RequestMethod.GET)`. It maps HTTP GET requests to specific handler methods.

### 4. @RequestParam Annotation
`@RequestParam` binds a web request parameter to a method parameter. It can extract query parameters, form data, etc.

### 5. Model Object
The `Model` interface provides a way to pass data from the controller to the view. Attributes added to the model are accessible in the Thymeleaf template.

### 6. MVC Pattern
- **Model:** Data passed via the `Model` object (the `name` attribute)
- **View:** The Thymeleaf template (`greeting.html`)
- **Controller:** `HelloController` handles requests and coordinates between model and view

---

## Static Resources

The application serves static resources from the `src/main/resources/static/` directory:
- `favicon.png` - Website favicon
- `images/vistula.png` - Vistula University logo (300px width)

---

## Testing

### Manual Testing in Browser
1. Start the application
2. Open browser and navigate to:
   - `http://localhost:8080/` - See plain text response
   - `http://localhost:8080/greeting` - See HTML view with default name
   - `http://localhost:8080/greeting?name=YourName` - See HTML view with custom name

### Testing with Postman/Swagger
- Use GET requests to test both endpoints
- For `/greeting`, test with and without the `name` query parameter

---

## Author

**Sagar**  
Student at Vistula University

---

## Repository

This project is part of the Spring Framework course assignment and is available on GitHub.

---

## Notes

- The application runs on port 8080 by default
- The H2 console is not configured for this task (that's part of Task 2)
- All endpoints use GET method as specified in the requirements
- The application demonstrates both direct response (`@ResponseBody`) and view rendering (Thymeleaf)

