Bind mounts are really useful when we want make changes in the code and we want to see them live. With bind mounts we deploy our app by mounting the code placed in the host to the container.

For example clone this [github project](https://github.com/BretFisher/udemy-docker-mastery) and cd to the `bindmount-sample-1` directory. From that directory run:

`docker container run -p 80:4000 -v "$(pwd):/site" bretfisher/jekyll-serve`

This will run a page with jekyll, in your `localhost:80`. In the `_posts` folder you can edit the file and by refreshing the browser you'll immediately see the changes.