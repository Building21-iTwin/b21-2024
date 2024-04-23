# App Deployment

## Overview

Now that you have a working application we can deploy it to the internet.

There are tons of ways to deploy applications. Because this is a very important operation, we don't want to mess it up. We want a reliable way to get code from our machines to "the cloud."

Luckily there are many services and types of software to aid in this task. We're going to use a fairly modern cloud service named Netlify.

Now, you might think one step in deploying would be to copy your files from your computer to the server. Some websites and apps are assuredly still deployed that way, but a significant problem with this is that it assumes the most-recent copy of code is on your computer. This _might_ be fine if you're the only developer on a project, but consider what happens if you're stuck somewhere without access to that machine. Or it may have broken.

A better way to get your code onto a server is to `push` your code into a git repository, and then have your deployment machine `pull` the code from there. Good news! You already have your code in GitHub and Netlify will help us do the rest.

## Ensure your app builds locally

First, let's double check that your app builds locally.

`npm run build`

If that succeeds, you're ready to go.

## Sign up for an account at Netlify

1. Go to [Netlify.com](Netlify.com) and click "Sign up"
2. On the next page, click the "GitHub" button to use your GitHub account to sign up and complete the sign in process.

## Create Netlify project

1. Once logged into Netlify, click the "Sites" link. On the page that opens, click "Add New Site" and then "Import from an existing project"
2. On the import page, click the "GitHub" button and Netlify will connect with your GitHub account. Follow the prompts and set Netlify app to have access to your app repository when asked.
3. After the GitHub - Netlify setup, you should see your repository available to select. Select it.
4. The next screen allows you to configure how your application will be built from the repository.
   - Don't change the owner if the option is available.
   - For now, keep the _branch to deploy_ as `main`, but you can imagine it might be useful to have a dedicated git branch for each version of your app you want to release.
   - The 'base directory' can remain blank as the root level of your repo is also your base directory.
   - The build command is also fine to leave as `npm run build` - it's a standard so Netlify has guessed correct once again.
   - Aha! Netlify is finally wrong. Our build directory is not 'dist/' but rather 'build/'. Please change it.
5. While we do have some more configuration to do, we'll need our deployed app's url, so let's click **Deploy Site** and hope for the best.

> [Alternative instructions](https://medium.com/itwinjs/deploying-the-itwin-viewer-to-a-web-host-d45c5cfdf0cf)


### What's happening?

Behind the scenes, Netlify is pulling in the code from your repo (with your permission, of course), building it using the command you specified, and then hosting the built site from the `/build` directory. It's able to do this because Netlify specializes in building and running javascript applications - it knows how to parse our package.json and ensure it has the necessary dependencies to build these apps. It then runs some sort of webserver to host the built files. That's an oversimplification of course, but it's good to have an idea of what's going on.

Netlify is just one service, of course. There are many places and ways to deploy applications, some which are specialized for a particular type of application, and some which are more general. The more general, the more configuration and setup you have to do.

## Let's see our app in action

After your app has built, you should see a button "Open Production Deploy." Click it.
Hmm... this isn't exactly what we expected. A white screen. Right click and select 'inspect' to open developer tools. (This is the first thing you should do if your application doesn't load properly!) You should see an error: "Please add a valid OIDC client id to the .env file and restart the application. See the README for more information." Oh right, the rest of the configuration.

## Add Netlify Configuration

- Go back to Netlfy. Click on the name of your app which Netlify has assigned randomly (mine was 'illustrious-meringue-7f8864') and then click on "Site Settings".
- In the left sidebar, click "Environment variables"
- Click the "Add a variable" dropdown, then select "import from a .env file"
- Open your .env file in vscode. Select all and copy the contents. Paste them into the "contents of .env file" text box.
- We need to modify two of these, the `IMJS_AUTH_CLIENT_REDIRECT_URI` and the `IMJS_AUTH_CLIENT_LOGOUT_URI` variables. Replace the `http://localhost:3000` part of each variable with the url which netlify has provisioned for your app. You can find it in that box toward the top of the screen - it should end in "netlify.app". You'll also have to add https:// to the beginning. You should have something similar to:

`IMJS_AUTH_CLIENT_REDIRECT_URI = "https://illustrious-meringue-7f8864.netlify.app/signin-callback"`

and

`IMJS_AUTH_CLIENT_LOGOUT_URI = "https://illustrious-meringue-7f8864.netlify.app/logout"`

Leave the rest of the options the same and click "import variables".

## Modify App Configuration

**Note this will be handled by a instructor**

We still need to do one thing before we can redeploy our app and see it live on the web. We need to tell our app's configuration about the new URLs we've just registered, otherwise we won't be able to sign in.

- Go to https://developer.bentley.com
- Login and then click "My Apps"
- Select the app you've created
- In the details box, click the `+` next to the present redirect URL.
- In the new field, enter the IMJS_AUTH_CLIENT_REDIRECT_URI you entered above.
- Do the same but for the post logout redirect URI.
- Click "Save" at the bottom of the screen.

## Redeploy your app

We need to redeploy the app to pick up on the newly added environment variables.

- Go back to Netlify. Click on "Deploys" from the navigation bar at the top.
- Click on the "Trigger Deploy" dropdown and select "Deploy Site"
- There's a game you can play while it builds. It is concentration/the match card game.
- See you're not not working, you're just building your app. [This used to take much longer and still does for many types of applications](https://xkcd.com/303/).
- Eventually it will be done - you can head back to your app and reload. Eventually it should redirect and prompt you to login, and then....
- Oh no! An error. So everything has not gone smoothly. Seems like Netlify doesn't know what to do with the /signin-callback path. We can fix that.

## Adding a simple redirect

Go back to your app in VSCode. Create file named `netlify.toml` in the root of your repository. Add the following contents (everything inside of the toml code block)

```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

See if you can complete the last steps on your own:

- Use git to commit your change
- Use git to push your change
- Go back to the dashboard in Netlify. You'll see your app is building again! By default, Netlify builds your application whenever a new commit is pushed to your repo.
- Okay, when it's finished, reload your page and hopefully see your app deployed on the web.
