# Developing **portfolio** with *react, sanity and tailwind* 

## Steps: 
1. Create a react project  
`npx create-react-app portfolio`  
1. Install sanity cli  
`npm install -g @sanity/cli`
1. Login with sanity cli  
`sanity login`
1. Create a sanity project   
`sanity init`
1. Add node modules in the .gitignore
1. Create a new repo on GitHub  
1. First commit to project  
`git init`  
`git add .`  
`git add origin remote link`  
`git push origin` 
1. Install sanity client with npm  
`npm install @sanity/client`
1. Create a *client.js* file for connecting our react project and sanity project  
1. Initialize `sanityClient` in client.js using **project-id** given inside sanity project i.e in *sanity.json*  
1. Add `localhost:3000` in CORS origin in the settings of sanity studio console for authentication {trusted urls}  
1. Do the second commit   
1. Install tailwindcss from the website  
    1. Search for installation  
    1. Copy the href link and paste it in the `index.css` file   
    1. Copy the href link of typography and do the same  

1. Add Google fonts from the website by importing it to the `index.css` file  
1. Add all the css properties in `index.css`  
1. Create a new folder in *src* folder named *components* which will have all the different pages  
1. Add `About.js, Home.js, NavBar.js, Post.js, Project.js, SinglePost.js` files in the components folder  
1. For routing from one component to another we need some routing  
1. So we install react-router  
`npm install react-router-dom`  
1. Import `BrowserRouter, Route, Switch` in `App.js`  
1. Import all components and Create routes for all the components in `App.js`  
1. Make a default *HTML* template to check for routing  
1. Do the third commit for routing added
1. Add *css* and *HTML* in the `NavBar.js` as per the requirements  
    1. Using `NavLink` from `react-router-dom` we implement NavBar
    1. Install `react-social-icons` package for including social media icons in the website   
    `npm install react-social-icons`  
        1. Import `SocialIcon` from `react-social-icons`
        1. Use the icons in the new `div` with specifying the network or the profile url
1. Do the fourth commit for navbar added  
1. Add the *HTML* contents in the `Home.js` for developing the home page  






# References
**Error** : `Attempted import error: 'About' is not exported from './components/About'.`  
https://stackoverflow.com/questions/53328408/receiving-attempted-import-error-in-react-app  










