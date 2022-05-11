# Espresso

## What Is AWS Amplify:

AWS Amplify is a set of purpose-built tools and features that lets frontend web and mobile developers quickly and easily build full-stack applications on AWS,
with the flexibility to leverage the breadth of AWS services as your use cases evolve.With Amplify, you can configure a web or mobile app backend,
connect your app in minutes, visually build a web frontend UI,
and easily manage app content outside the AWS console. Ship faster and scale effortlessly—with no cloud expertise needed.

![image](https://user-images.githubusercontent.com/97823170/167903282-300602ec-b7df-4d6d-a693-31d6c4d786f8.png)

![image](https://user-images.githubusercontent.com/97823170/167903464-5e0c7df6-a91c-4800-b91c-76ebf62b357a.png)

![image](https://user-images.githubusercontent.com/97823170/167903495-ec2ef76e-2e01-463d-bc40-6eef8787a327.png)

## Amplify Hosting features:

Amplify Hosting supports the common SPA frameworks, for example, React, Angular,
Vue.js, Ionic, and Ember, as well as static site generators like Gatsby, Eleventy, Hugo, VuePress, and Jekyll.

Manage production and staging environments for your frontend and backend by connecting new branches. See, feature branch deployments.

Connect your application to a custom domain. See, set up custom domains.

Deploy and host SSR web apps created using the Next.js. framework.

Preview changes during code reviews by setting up pull request previews.

Improve your app quality with end to end tests. See, end-to-end testing.

Password protect your web app so you can work on new features without making them publicly accessible. See, restricting access.

Set up rewrites and redirects to maintain SEO rankings and route traffic based on your client app requirements. See, using redirects.

Instant cache invalidations ensure your app is updated instantly on every code commit.

Atomic deployments eliminate maintenance windows by ensuring that the web app is updated only after the entire deployment finishes.
This eliminates scenarios where files fail to upload properly.

Get screen shots of your app rendered on different mobile devices to identify layout issues.

***Q: How is hosting a modern web app different from a traditional web app?***

Hosting a modern web app does not require web servers and can use content delivery networks to store static content (HTML, CSS and JavaScript files).
AWS Amplify leverages the Amazon CloudFront Global Edge Network to distribute your web app globally. 

![image](https://user-images.githubusercontent.com/97823170/167904955-4b99a5a8-579e-432b-ac4a-40d37751ef44.png)

**Getting started with Amplify Hosting**

To get started with Amplify's hosting features, see the Getting started with existing code tutorial. After completing the tutorial
, you will be able to connect your git repository (GitHub, BitBucket Cloud, GitLab, and AWS CodeCommit) to set up continuous deployment. Alternatively,
you can get started with one of
## Amplify Studio:
You can access Amplify Studio from the AWS Amplify console in the AWS Management Console.
Amplify Studio is a visual development environment that simplifies the creation of scalable,
full-stack web and mobile apps. Use Studio to build your frontend UI with a set of ready-to-use UI components, create an app backend,
and then connect the two together. See the user guide for Amplify Studio in the Amplify docs.

***Q: What happens when a build is run?***

AWS Amplify will create a temporary compute container (4 vCPU, 7GB RAM), download the source code, run the commands configured in the project, deploy the generated artifact to a web hosting environment, and then destroy the compute container. During the build, AWS Amplify will stream the build output to the service console.

![image](https://user-images.githubusercontent.com/97823170/167904993-75fdb394-d2c3-4669-ba0e-3d6ab74c7298.png)

## Amplify Studio features
Visual data modeling enables you to focus on your domain-specific objects instead of cloud infrastructure.

Set up authentication for your app.


Powerful and easy to understand authorization.

Infrastructure-as-code configures all backend capabilities with AWS CloudFormation.

Works with the Amplify Command Line Interface (CLI). All updates you make in Studio can be pulled into the CLI.

Invite users via email to configure and manage the backend. These users will also be able to log in to the Amplify CLI with their email.

Content management with markdown support.

Manage users and groups for your app.

Use Studio's visual designer to build frontend UI components. Choose from dozens of designs in the pre-built UI component library.

![image](https://user-images.githubusercontent.com/97823170/167905152-4be3fb31-e7d8-4703-8ad9-2b42829c5583.png)

Import Figma prototypes built by designers into Studio as React code.

Customize your frontend UI with themes to apply global styles to your app's components.

Configure and test your UI components directly within Studio to see how they update and display data.

Bind your cloud-connected backend to your frontend UI in a few simple steps.

***Q: What are atomic deployments?***

Every deployment is atomic, which means the site is ready to view after the deployment is complete. Atomic deployments eliminate maintenance windows by ensuring the
web app is only updated once the entire deploy has finished. The new version of the web app is then made available instantly to end-users,
without the developer having to invalidate CDN caches.

## Getting started with Amplify Studio:

You don't need an AWS account to get started using Studio to create a backend. Without an AWS account, you can begin modeling data for your backend locally.

With an AWS account, you have access to an expanded set of Studio features for managing your backend environment as well as the visual designer for creating
frontend UI components that you can connect to your app's backend. For more information.

***Q: How can I leverage AWS Amplify web hosting to work with multiple environments?**

AWS Amplify leverages Git’s branching model to create new environments every time a developer pushes code to a new branch. In typical development teams, developers deploy their ‘master’ branch to production, keep the ‘dev’ branch as staging, and create feature branches when working on new functionality. AWS Amplify Console can create frontend and backend environments linked to each connected branch. This allows developers to work in sandbox environments, and use ‘Git’ as a mechanism to merge code and resolve conflicts. Changes are automatically pushed to production once they are merged into the master (or production) branch.


## Modern SPA web applications:

This user guide is intended for customers who have a basic understanding of modern single-page web applications (SPA). Modern web applications are constructed as SPAs that package all application components into static files. Traditional client-server web architectures led to poor experiences; every button click or search required a round trip to the server, re-rendering the entire application. Modern web apps offer a native app-like user experience by serving the app frontend, or user interface, efficiently to browsers as prebuilt HTML/JavaScript files that can then invoke backend functionality without reloading the page.

A modern web application's functionality is often spread across multiple places, such as databases,
authentication services, frontend code running in the browser, and backend business logic, or AWS Lambda functions,
running in the cloud. This makes application deployments complex and time-consuming as developers need to carefully coordinate deployments 
across the frontend and backend to avoid partial or failed deployments. Amplify simplifies deployment of the frontend and backend in a single workflow.

***Q: What are environment variables? How do I use them?***

Environment variables are configurations required by apps at runtime. These configurations could include database connection details, third-party API keys, different customization parameters and secrets. The best way to expose these configurations is to do so with environment variables. You can add environment variables when creating an app or by going to the app settings. All environment variables are encrypted to prevent rogue access. Add all your app environment variables in the key and value textboxes. By default, AWS Amplify applies the environment variables across all branches, so you don't have to re-enter variables when you connect a new branch. Once you enter all the variables hit Save.
