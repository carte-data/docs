# Setting up the admin site

The admin site that comes built into Carte is a Netlify CMS instance. By default, each dataset page contains an `Edit` link, that takes you to the corresponding Netlify CMS page, where you can edit (and commit back) the descriptions for the given dataset and its columns.

For this to work, you need to authenticate with your GitHub account, since the CMS will commit changes under your name. This only works with an OAuth server, which Netlify provides (if hosted on their platform). For other scenarios, you can host your own using [any of the options listed in the [CMS' docs](https://www.netlifycms.org/docs/external-oauth-clients/). There's also a great tutorial [here](https://dev.to/bbenefield89/create-your-own-serverless-oauth-portal-for-netlify-cms-afk) about setting up your own Node.js OAuth server. 

I'm also working on a hosted Carte OAuth server that's a drop-in replacement.

To set up the admin site, you need to change the `backend` section in the CMS config file at `content/admin/config.yml`. The available options can be found in the [CMS docs](https://www.netlifycms.org/docs/backends-overview/).

