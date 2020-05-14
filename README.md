# Sass import and exports
Recently I ran in to an issue where I had a custom css framework (designed by the one and only @stowball), but I needed to share the styles between different projects. The issue was I did not need the whole style defintion of a component in the second project but the framework was not built to have that support. So this repo is my proposed solution to the issue, where I have used sass mixins to provide a way of importing and exporting specific css classes. 

## To install and run 
Clone the repo, and then install using the commands: 

`yarn install` or `npm install`
 
 Then simply run: 
 
 `yarn build` or `npm build`
 
 Observe the dist folder
 
 ## The science of the theory
 In javascript there is the concept of import and export, where if a developer wanted, you can export a particular constant or function, which means another javascript file can import those values when they need them and not import useless code. Im not going to go in to the finer details of that here. With sass there is no "export" as such. 
 
 Traditionally with sass you put you styles for a component in a partial, lets use the classic example of card. The card partial will look something like this: 
 
 ```
 .card {
  background: white;
  padding: 0.5rem; 
}

.card-title {
  color: blue;
  font-size: 1.1rem; 
}

.card-text {
  color: gray;
  font-size: 0.8rem; 
}
```
You would then import this file into where ever required, some `all.scss` file.

However, in my instance, I had a new project I had to build for where it shared almost the same styles as the framework. In some instances for a component I only needed some classes of a component. So for example the new project only needed `card-title` of the `card` component, for me to get that class I would need to import the entire `card` partial. And just to make it more important, lets say I needed to make the css file size for the new project as small as possible (the limit is 75kb, you can work out what the project is). 

So in this project what I have done is make every class a mixin, that way we can import the entire framework into a project but we only import or `include` the classes that we need. If we just need the whole file, I created an `all` mixin of that component. 

## Summary
This method has been designed to share styles between a framework, and only include what we need. This way we can reduce the size of our css for a project and reduce the unused css classes without the need for tools like css purge. 
