## Upvote

Upvote is a Reddit-esque web application that allows users to create posts, upvote and downvote posts, and comment on posts in a multi-threaded, nested list.

The project is built using Next.js with the /app router and [Tailwind CSS](https://tailwindcss.com/), and uses [Auth.js (formerly Next Auth)](https://authjs.dev/) for user authentication. The data is stored in a Postgres database, which is created and accessed with raw SQL queries using the `pg` package.

The project is a work in progress and is not yet complete.

## Features

- [x] View a list of posts
- [x] View a single post
- [x] Create a post
- [x] Upvote and downvote posts
- [x] Pagination of posts
- [x] Comment on posts
- [x] Nested comments (recursive lists)
- [x] User authentication

## Setup instructions

1. Fork the repository (check "copy the main branch only") and clone your fork to your local machine
2. Run `npm install`
3. Create a `.env.local` file in the root directory and add the following environment variables:
   - `DATABASE_URL` - the URL of your Postgres database (eg. the Supabase connection string)
   - `AUTH_SECRET` - the Next Auth secret string (this can be anything at all like a password, but keep it secret!)
   - `AUTH_GITHUB_ID` - the GitHub OAuth client ID (create yours in [Github developer settings](https://github.com/settings/developers)
   - `AUTH_GITHUB_SECRET` - the GitHub OAuth client secret (create this in [Github developer settings](https://github.com/settings/developers))
4. Create the database schema by running the SQL commands in `schema.sql` in your database (eg. by running the commands in Supabase Query Editor)
5. Run `npm run dev` to start the development server
6. Open [http://localhost:3000](http://localhost:3000) with your browser to see the site

## Potential future features

- [ ] User profiles
- [ ] Sorting posts by recent (date posted), top (most upvotes), and most controversial (most upvotes _and_ downvotes)
- [ ] User karma scores
- [ ] User badges / trophies (awards for achievements like number of posts, years on the site, etc.)
- [ ] User settings (eg. number of posts per page, theme, etc.)
- [ ] Moderation tools / reporting or flagging objectionable comments for removable by admins
- [ ] Searching posts (possibly using simple SQL LIKE '%some search%', or [Postgres text search](https://www.crunchydata.com/blog/postgres-full-text-search-a-search-engine-in-a-database))
- [ ] Subreddits (separate communities, that isn't just one big list of posts, that can be created by users)
- [ ] User notifications
- [ ] User private messaging
- [ ] User blocking
- [ ] User following
- [ ] User feed (posts from users you follow)
- [ ] User flair

CORINNA DEVLOG
Started the project by forking and then cloning down the repo. Deployed to Vercel as my first step - felt instantly suspicious that there were no errors that prevented the deployment. Now going to watch the vide3o provided on moodle about the github stuff. Watched the video through, sat on it for a moment pondering the secret keys folder then remembered the moodle said we would need to set up those folders so went back to the moodle page to read everything through. Joe appeared - harbringer of errors and pointer of problemtic though processes - and pointed out that I hadnt visited the deployment - I did and it came up with an error (blerrrrrhhh). So Joe reminded me to start with the stuff I know how to do, like creating a database schema and getting the database secret key.
Supabase needs to calm down pausing my databse - I don't want pro and I just need you to sit there until I'm ready to use you again.
Copied the schema inputs from the schema file into supabase and went through running each table to create them - ran into a error with having previous tables with the same name. Googled if there was a way to ignore them but google through the words 'disable' and 'partion' around and that sounds scary for something we havent learnt. Asked Bertie for help, and he recommended just renaming the tables and then altering the text to accomodate the chang . He also showed me the 'search' and 'replace' features which will help me do this in VS Code.
Changed two of the table names and wrote down those changes in my physical notes for me to refer back to, then continued running the tables. Last table errored on syntax, checked the syntax through and found a stray commer - removed it and ran it again and it was successful.
Had a feeling I needed to check the schema so I did and realised that even though I'd changed the table names, I also needed to change the links between the tables to reflect the changed names as the tables were linking to my other tables with their Ids. Went back in and changed the Id names to the new names, deleted the tables and ran them again - no errors. Checked the schema again and saw two of the tables werent linked so asked Joe about if the reasons was because of a piece of missing syntax. He said I was going down a rabbit hole I didnt need to, but good thinking. Left that and set about changing my database password and retrieving the transaction pooler. Had to google where to find it because it wasnt where I though it was - found it, copied it then changed out the password and saved.
Did npm run dev to load the page and see what happens, it errored and linked the error to {session.user.name} which i think is to do with the changes to the table names I did. Tried changing them but error stayed the same, undid the chamnges and set about making the secret keys for github (thinking its a connection issue) so followed the steps in the youtube video to create the github secret keys and then added them to my env. file. With the database connection, and git hub connections added to the env file, i tried running local host again. Same error, tried to google the error but it didnt come up with a likewise working example of my issue - went to chat gpt and pasted the error in there and asked it to explain the issue to me. It pointed to an error with the connection to the database, so I went and redid the transaction pooler and secret key, didnt make a difference. Now think it might be a local host issue, the database running on the wrong local host but I'm not sure what to do about that so will ask Bertie.
Joe mentioned over lunch about changing over the URLs after deployment from local host to the deployed url. Changed them over but still erroring, asked for help with Bertie and we discovered I was using the wrong url - changed it and it still errored. Bertie reminded me I will need to push my code changes to github WHICH I COMPLETELY FORGOT WAS A THING. Along with forgetting to add the environment variables to vercel. Brain be doing me dirty forgetting the important factuals.
Page still erroring but this time on the DB qery saying it couldnt find specific content - asked Bertie for help and we serarched the DB query, and some of the names hadn't been changed to reflect the changes I made to the table names.
Push my code to git then redployed - login page is show, and I'm able to click on 'log on with github' the page then errors to this: 'The redirect_uri is not associated with this application. The application might be misconfigured or could be trying to redirect you to a website you weren't expecting.' I DONT UNDESTAND THIS ERROR, WHAT DOES IT MEANNNNNNN!
Still having issues with connecting, Joe and Bertie both came to help and saijd it must be because i changed the table names, and have suggested I create a new project in Supabase, create the schema again with the original schema used in the project and then do the whole repo again. SO....WE START AGAIN
