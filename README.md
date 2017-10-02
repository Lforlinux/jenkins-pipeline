
# Jenkins Pipes HelloWorld

Run docker images from the repo 

```bash
 docker run -d --rm --name jenkins     -p 8080:8080 -p 50000:50000     lforlinux/jenkinspipeline:version1
```

## How it works


The `Jenkinsfile` in here describes **HOW** this project is built, in terms of the individual stages that make up the build pipeline and what happens within them:

```groovy
node {
  try {
    stage('checkout') {
      checkout scm
    }
    stage('prepare') {
      sh "git clean -fdx"
    }
    stage('compile') {
      echo "nothing to compile for hello.sh..."
    }
    stage('test') {
      sh "./test_hello.sh"
    }
    stage('package') {
      sh "tar -cvzf hello.tar.gz hello.sh"
    }
    stage('publish') {
      echo "uploading package..."
    }
  } finally {
    stage('cleanup') {
      echo "doing some cleanup..."
    }
  }
}
```


# Pipeline Job
```
1)Choose Pipeline script from SCM
2)SCM as GIT 
3)Repo URL : https://github.com/Lforlinux/jenkins-pipeline.git
4)Select */master branch to build
```

## Where to go from here?

Now that you have a minimal example running, here are some ideas on how to dig further:

 * go and explore the [Pipeline-DSL](https://jenkins.io/doc/book/pipeline/syntax/) and [Steps Reference](https://jenkins.io/doc/pipeline/steps/)
 * add email notifications on success / failure
 * create a similar helloworld example in your favorite programming language
 * use node labels to run your builds on specific nodes only
 * try modeling more complex pipelines with parallel execution etc
 * ...
