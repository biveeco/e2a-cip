# Get Started
1) Install [yarn](https://yarnpkg.com/lang/en/)
2) In the root of this directory run `yarn install` to install dependencies
3) Run `yarn serve` in the root dir to run a server on localhost
4) Go to `localhost:8080` to view the app
5) To package the app for desktop use run `yarn build:electron --windows` or `yarn build:electron --macos` (the final files will be in the `/dist_electron` folder)
6) To package the app for hosting use run `yarn build` (the final files will be in the `/dist` folder)

# Editing Content
To edit content you can click [here](https://github.com/E2A/e2a-cip/blob/master/src/locales/en.yaml)

It uses Markdown - you can test your text [here](http://miaolz123.github.io/vue-markdown/)

To add resources and other files you can upload them to `public/uploads` you can access it [here](https://github.com/E2A/e2a-cip/tree/master/public/uploads)

# Data Structure / ERD
We are using [Vuex ORM](https://vuex-orm.github.io/vuex-orm/) for data management.

Edit ERD by going to [draw.io](https://draw.io) and upload the [E2A_ERD.xml](/docs/E2A_ERD.xml) file.

### ERD Diagram for Application
![ERD](docs/E2A_ERD.png)
