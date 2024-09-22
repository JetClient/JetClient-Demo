# JetClient Demo

[JetClient](https://plugins.jetbrains.com/plugin/21173-jetclient--the-ultimate-rest-client) is a plugin for JetBrains IDEs that allows you to develop, test, and debug your APIs effectively. It uses `.md` files to store requests and folder data, making it easy to share and collaborate on API development.

This demo project is based on the [Spring PetClinic REST Sample Application](https://github.com/spring-petclinic/spring-petclinic-rest). The project contains an [openapi.yml](openapi.yml) file with the API specification and a [.jetclient](.jetclient) folder with JetClient sync files.

## How to Try It Out

### Prerequisites

- JetBrains IDE (IntelliJ IDEA, WebStorm, PyCharm, etc.)

### Steps

1. **Install JetClient Plugin:**
    - Open your JetBrains IDE.
    - Go to `Settings` -> `Plugins` -> `Marketplace`.
    - Search for `JetClient`.
    - Install the JetClient plugin and restart your IDE.

2. **Clone the Repository:**
    - Clone the JetClient-Demo repository to your local machine using the following command:
       ```shell
       git clone https://github.com/JetClient/JetClient-Demo.git
       ```

3. **Open the Project in the IDE:**
    - Open the cloned project in your JetBrains IDE.

4. **Import JetClient Project:**
    - Open the JetClient tool window.
    - Click the plus icon on the toolbar and select `Import` -> `JetClient project`.
    - Ensure the path to the `.jetclient` folder is correct and click `Add`.

5. **Explore Requests and Tests:**
    - In the JetClient tool window, you will see the imported project with requests and test suites.
    - You can open and run requests and tests from here.

### How to Run the PetClinic Application in Docker

To start the PetClinic server using Docker, run the following command:

```shell
docker run --name petclinic -p 9966:9966 springcommunity/spring-petclinic-rest:3.2.1
```

This command will pull the PetClinic REST image from Docker Hub (if not already pulled) and run the server on port 9966.