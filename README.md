# Angular4-tests
This is to explain how to write e2e tests for angular 4 app, which uses external service to get data to be displayed.

# Goal:
To write e2e tests for angular4 application. This Angular 4  application uses an external web service which returns a json data.  

# Libraries/base projects used:
Angular-seed

additional library:
https://www.npmjs.com/package/gulp-mock-server
https://www.npmjs.com/package/gulp-protractor


# Description

The angular-seed project here has test files in e2e/component.e2e.ts
E2e tests should run independant of the background service to achive that, use gulp-mock-server to create mock server of the backend service.
Set an ip for the backend mock server in gulpfile.ts 
e.g.
 
``` 
gulp.task('mock', function() {
  gulp.src('.')
    .pipe(mockServer({
      port: 8090,
      allowCrossOrigin: true
    }));
});
```

In this case backend mock server uses port no 8090. 
Now mimic the data it which is been sent by web service on an action of Angular 4 app.
for e.g. if data is coming from service 
http://websrevice/records/<id>

For the following record the call looks like 
http://websrevice/records/12345

Create a /records/1234.json directory structure under /data directory at root of angular app.
```
  data
    \records
      \1234.json
```

Angular-seed  has some predefined set of commands which are used to run tests. 
For e2e tests we need to make sure the mock server is running and angular application is using the proper this mock service to test applications.
in the agular-seed seed-tasks.json creates the sets of commands and to override those use project-tasks.json
```
{
  "test": [
    "build.test",
    "karma.run"
  ],
  "serve.e2e": [
    "mock",
    "build.dev",
    "build.js.e2e",
    "server.start",
    "watch.dev",
    "watch.e2e"
  ]
}
```

Angular-seed project uses package.json to define the commands for different tasks defined above.

In this example assets/env.js  file sets the env variables for angualr application.
Make sure to put proper service-api url for testing e.g . http://localhost:8090/ 



# Some other references if needed (Not required for this project):
https://oliverveits.wordpress.com/2017/09/12/angular-e2e-protractor-tests-on-systems-without-gui-applied-to-static-and-dynamic-web-pages/

https://coryrylan.com/blog/introduction-to-e2e-testing-with-the-angular-cli-and-protractor

https://stackoverflow.com/questions/40300272/cannot-find-module-tmp-rx-min-js

https://angular.io/guide/testing#get-injected-services

https://www.udemy.com/testing-angular-apps/learn/v4/t/lecture/7052130?start=0
