#An API for UMD data

Status: We are live at [umd.io](http://umd.io)

##TODO:
###Docs:
  - license and copyright?
  - Tutorials for using the API with different languages
  - Styling: font-size, nav float on pages, list styles in description section
  - mobile menu
  - Bus
    - Route schedule
    - Route arrivals
    - Route locations
    - List Stops
    - Get Stop
    - Locations
  - Courses
    - Semester
  - Map
    - Buildings

###Implement:
  - add query capability (e.g. /courses/ENES100?instructor=Calabro)
  - allow limits and filters -- projection stuff
	- courses/search
    - paginate responses
	  - courses/<dep>
  - namespace the routes or use a controller scheme
  - expand:
    - sections works
    - stops?
    - courses?

###Testing:
  - Remove hardcoding from tests
  - maps
  - buses
  - Unit tests for methods - particularly helpers
  - break tests out into features - a file per endpoint gets unwieldy
  - production tests
  - tests for docs? alerts for when the site is down? Something!

###Future Endpoints:
  - [Buses](http://api-portal.anypoint.mulesoft.com/nextbus/api/nextbus-api)
  - Finals for Courses
  - [Maps + Buildings](http://maps.umd.edu/arcgis/rest/services)
  - Budget - this is kinda hard
  - CAS
- optimizations: cache responses (eventually, we might move to metadata + pagination)
- Refactor [this way?](http://stackoverflow.com/questions/5015471/using-sinatra-for-larger-projects-via-multiple-files)

Meta: find developers and projects, eat more databases, build core team, think about long term (license, technology, team structure)

##Contributing: Getting Started
Depending on where you are starting from, should take between 10 minutes and forever

-  (mac) install [xcode command line tools](https://developer.apple.com/xcode/) (or `xcode-select --install` from the command line)
- (mac) install [homebrew](http://brew.sh/)
- install [git](http://git-scm.com/) (or `brew install git`)
- install [rvm](https://rvm.io/rvm/install)
- install [node and npm](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager)
- install ruby 2.2.0 and switch rubies `rvm use 2.2.0`
- install [mongodb](http://docs.mongodb.org/manual/installation/)
- git clone this repo `git clone https://github.com/umdio/umdio my_umdio_app_folder`
- install bundler to manage dependencies `gem install bundler`
- install and build all the dependencies `bundle install`

Warning! If you are running other mongodb databases or rack servers, don't use the rake commands. Or, if you are on a system (i.e. production server) where you ought to run mongo independently, do that instead of using rake.

- build the database `bundle exec rake setup`
- start a local server `bundle exec rake up`
- run the test suite `bundle exec rake`
- check development at localhost:3000

If you get sick of typing `bundle exec rake` all the time, alias it to something short like `r`.

- Stop and start the database with `bundle exec rake database:down` and `bundle exec rake database:up`

If you are working on the documentation, move into the docs folder with `cd docs` and `make`. Then, to serve the docs locally, use `jekyll serve` and view on [port 3000](localhost:3000).

##Contributing:Development Workflow
- Design the endpoint you want to create, e.g. /bus
- Write initial 'hello world' tests in the tests/ folder in a file named something like buses_spec.rb
- Run the tests with `bundle exec rake` (alias it to `r`, you'll need it a lot). Your initial tests should fail.
- Create a bus folder with bus.rb and bus_helpers.rb, using the module structure from similar files (see courses)
- require and register your module in server.rb
- add routes of the form "app.get '/<endpoint>'""  to the module
- add hello world code, hello world tests should pass

write tests --> add functionality --> make tests pass --> write tests

- document the new functionality.
- Add a folder to the docs/src/ directory with the name of your endpoint. Put method documentation in a \_posts folder inside it. Look at the documentation for courses in src/courses/\_posts for examples.
- Add a page for the endpoint in the docs/src folder named something like buses.md
- write the introduction to your endpoint in the <endpoint>.md file, and the methods in the _posts folder.

##Contributing:Read more
- [Design doc](https://docs.google.com/document/d/11uslF3ftvQ3It-NRXs7iRgI34S0MxvqV2S1jioXPcL0/edit?usp=sharing)
- [Ideas doc](https://docs.google.com/document/d/1WQ4w4_HSdkzNP1j0KqrHSYtiU8DEGoXnxHyC5FEp5sY/edit)
- [Sinatra](http://www.sinatrarb.com/)
- [Rack](http://rack.github.io/)
- [MongoDB](http://www.mongodb.org/)
- [RSpec](http://rspec.info/)
- [Nginx](http://nginx.org/en/docs/)

###Notes:
- Security:
  - We should thoroughly test our system's security from the beginning, and have evidence that we are secure - that way, more people can trust us with their data!
  - Eventually, a single API for UMD data is much less vulnerable than a thousand separate databases everywhere - do it right once, enforce it strictly, then you only have one thing to worry about. Defense in depth, lock everything tight. Open is more secure than closed, because you have more eyes on it.
