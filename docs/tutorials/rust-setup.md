# Setting up a dev container for Rust

* Primary author: [Yueen Ma](https://github.com/myueen)

* Reviewer: [Malak](https://github.com/malaksoubai)

## Introduction :heart:

Hello! Welcome to the tutorial for creating a new project in dev container for Rust! I am excited to take you on this journey to learn step-by-step how to make your own Rust-specific dev container. 

Rust is one of the most popular programming language for web development. It is known for building high-performance servers and APIs. Setting up a docker container for Rust would speed you up in onboarding and start coding in Rust! Before diving into the details of setting up the dev container, we make sure you have the prerequiesites satisfied in your local computer. 


## Prerequisites
- Sign up at [GitHub](https://github.com/) if you don't have an account already. 

- Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). 

- Download and install [Visual Studio Code](https://code.visualstudio.com/) (VS Code). 

- Install [Docker](https://www.docker.com/products/docker-desktop/)

- Understand Command-line basics. 


## **Setting up for the Project**

## Git Repository Setup
In this section, we will create a local repository for this project and link it to GitHub. 

1. Open your terminal or command prompt, and create a new directory **comp423-rust** using the following commands: 

    ```console
    mkdir comp423-rust
    cd comp423-rust
    ```

    !!! note "Create a New Directory"
        This step will create a folder comp423-rust in your home directory. If you want this folder elsewhere, go ahead and change to that parent directory first. 

 
2. Initialize a new Git repository and create a README file: 

    ```console
    git init
    echo "# Setting up Rust dev container" > README.md
    git add README.md
    git commit -m "Initialize commit with README"
    ```


3. Create remote repository on Github: 
    - In Github, log in and navigate to [Create a New Repository](https://github.com/new) page
    - Fill in the following details: 
        - **Repository Name**: comp423-rust
        - **Description**: "Rust dev container for coding in Rust"
        - **Visibility**: Public
    - Leave the rest options as it is and Click **Create Repository**


4. Link local repository to Github
    - Open your terminal or command prompt, and add the GitHub repository as a remote. *Note*: Change ```<your-username>``` with your GitHub username. 

    ```console
    git remote add origin https://github.com/<your-username>/comp423-rust.git
    ```

    - Use ```git branch``` to check default branch name. 
        - If default branch name is not ```main```, use the following conmand to rename: ```git branch -M main```

    - Push your local commits to Github repository:

    ```console
    git push --set-upstream origin main
    ```
    !!! Note on --set-upstream flag
        The --set-upstream flag sets up main branch to track remote branch. It allows you to just write ```git push origin``` in future pushes and pull without specifying ```main``` branch. 

    - To view your changes, you can refresh GitHub repository or use ```git log``` in terminal/command prompt to see the commit. 




## Dev Container Setup
In this section, we will create a dev container for Rust! 

1. Add Development Container Configuration
    - Go to VS Code and open ```comp423-rust``` directory. 
    - Install the **Dev Containers** and **rust-analyzer** extensions for VS Code. 
    - Create a ```.devcontainer``` directory in the root of your project with the following file inside this "hidden" configuration directory: ```.devcontainer/devcontainer.json```
    - Add the following content inside ```devcontainer.json```. 

    ```json
    {
    "name": "Rust Development Environment",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "rust-lang.rust-analyzer"
            ]
        }
    }
    }
    ```

2. Reopen the project in a VSCode Dev Container by pressing ```Ctrl+Shift+P``` (or ```Cmd+Shift+P ``` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may takes a few minutes while the image is downloaded and the requirements are installed.





## Initialize a Hello-World Rust Project 
1. Inside your ```comp423-rust``` folder and within the ```main``` branch, check Rust version using this commend: ```rustc --version``` in terminal or command prompt. It will display something like: 

```
rustc 1.83.0 (90b35a623 2024-11-26)
```

2. Run this following commands in your terminal (inside the container). This command creates a new directory and project called *hello_comp423*. Inside the *hello_comp423* folder, you will find a ```src``` folder and a file named ```main.rs```. 

    ```console
    cargo new hello_comp423 --vcs none
    cd hello_comp423
    ```

    !!! note "Note on ```---vcs``` none"

        The **```---vcs```** flag does not create a new ```git``` repository automatically on your behalf. 


    - The Cargo.toml file is called a manifest, and it contains all the metadata that Cargo needs to compile your pacakage. It will contains the following in this example: 

    ```
    [package]
    name = "hello_comp423"
    version = "0.1.0"
    edition = "2021"

    [dependencies]
    ```

    - Inside the ```src/main.rs```, write the following content:

    ```rust
    fn main() {
        println!("Hello COMP423");
    }
    ```
    



## Building and Running a Cargo Project
1. If you are not inside the ```hello_comp423``` directory, type in the following command ```cd hello_comp423``` to change the directory.

2. From your hello_comp423 directory, build your project by using the following command:  

    ```console
    cargo build
    ```
    
3. Compile the code and run the executable in this following command:

    ```console
    cargo run
    ```

If all goes well, this command should print out **"Hello COMP423"** in the terminal.

!!! note "Difference between ```cargo build``` and ```cargo run```"
    The command ```cargo build``` creates an executable binary file in your current directory. After that, ```cargo run``` compile and run the executable in one command. 

Congradulation on writing your first Rust program in a dev container! 




### Citations: 
1. Jordan, Kris. "Starting a Static Website Project with MkDocs," _COMP423 - Spring 2025_, https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-add-requirementstxt-python-dependency-configuration. 

2. Klabnik, Steve and Nichols, Carol, "The Rust Programming Language," https://doc.rust-lang.org/book/.