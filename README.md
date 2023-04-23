## Create-a-Jenkins-Shared-Library

### Technologies used:

Jenkins, Groovy, Docker, Git, Java, Maven

### Project Description:

Create a Jenkins Shared Library to extract common build logic:

Create separate Git repository for Jenkins Shared Library project

Create functions in the JSL to use in the Jenkins pipeline Integrate and use the JSL in Jenkins Pipeline (globally and for a specific project in Jenkinsfile)

Here's a step-by-step guide on how to create a Jenkins Shared Library using Jenkins, Groovy, Docker, Git, Java, and Maven.

Step 1: Set up Git repository for Jenkins Shared Library project

1. Create a new Git repository for your Jenkins Shared Library project. You can use any Git hosting service such as GitHub, GitLab, or Bitbucket.

2. Clone the empty Git repository to your local machine using the Git command line or a Git GUI client.

3. Create a vars directory at the root of the repository. This is where you will define your custom functions in Groovy script files.

Step 2: Define functions in Jenkins Shared Library

1. Inside the vars directory, create a Groovy script file for each custom function you want to define. The script file should have the same name as the function you want to define.

2. Write your custom functions using Groovy syntax. You can use any Groovy code, including importing external libraries, to define your functions. For example, you can define a function to build a Maven project as follows:

        def buildMavenProject(String projectDir) {
      // Run Maven command to build the project
      sh "cd ${projectDir} && mvn clean install"
    }
    
Step 3: Integrate Jenkins Shared Library in Jenkins

1. In your Jenkins instance, go to Manage Jenkins > Configure System.

2. Scroll down to the Global Pipeline Libraries section and click on the Add button to add a new library.

3. Enter a name for your library, e.g., "MySharedLibrary".

4. Choose the "Modern SCM" option and specify the Git repository URL for your Jenkins Shared Library project.

5. Optionally, you can specify a default version to use, or leave it blank to use the latest version of the library.

6. Click on the Save button to save the configuration.

Step 4: Use Jenkins Shared Library in Jenkins Pipeline

In your Jenkinsfile, you can now use the functions defined in your Jenkins Shared Library by calling them with the library name and function name, separated by a dot. For example:  

        @Library('MySharedLibrary') _
    pipeline {
      agent any
      stages {
        stage('Build') {
          steps {
            // Call the custom function from the Jenkins Shared Library
            buildMavenProject('/path/to/my/project')
          }
        }
      }
    }
    
Note: The @Library('MySharedLibrary') _ directive at the beginning of the Jenkinsfile tells Jenkins to load the "MySharedLibrary" globally, making the functions defined in the library available for use in any Jenkins pipeline.

That's it! You've now created a Jenkins Shared Library, defined custom functions in it, and integrated it into your Jenkins pipeline. You can continue to expand and enhance your Jenkins Shared Library by adding more functions and reusing them across multiple Jenkins pipelines to extract common build logic.
