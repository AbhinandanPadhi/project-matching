[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/dsc-umass/project-matching)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# project-matching

<!-- [![Build Status](https://travis-ci.org/abhinavtripathy/XAuth.svg?branch=master)](https://travis-ci.org/abhinavtripathy/XAuth) -->

<div><p align="center">
<center><h4>project-matching is supported & used by:</h4><a href="https://www.linkedin.com/company/dscntu/"><img width="270" src="assets/dsc_ntu.png" target="_blank"></a>
<a href="https://umassdsc.com/" target="_blank"><img width="270" src="assets/dsc_umass.jpg"></a>
<a href="http://www.dsc-rpi.club/" target="_blank"><img width="270" src="assets/dsc_rpi.png"></a>
</center></p></div>

Project Matching is an open source project that helps teams/clubs help match their members to projects. The application allows the admin to rank people's skills based on projects and then the team members rank projects, then the application matches people to projects based on the [stable match algorithm](https://en.wikipedia.org/wiki/Stable_marriage_problem). 

## Getting Started without Docker

### Prerequisites 

You would need ruby 2.7.0 and rails 6. Installation instructions are [here](https://gorails.com/setup/ubuntu/20.04)

You would also need postgres for this application. Installation instructions are [here](https://www.postgresql.org/download/)

### Setting up database connection 

To setup a database connection from the rails application, you need edit the env.yml file. 

```
DATABASE_USER: 'YOUR USERNAME'
DATABASE_PASSWORD: 'YOUR PASSWORD'
DATABASE_HOST: ''
```

Leave the database host empty. Use the same username and password that you used to setup postgres.

### Installing dependencies 

Use bundle and yarn to install dependencies.

```
bundle install

yarn install
```

### Setting up the database 

Setting up the database is a one time only thing when you first clone the rails application.

```
cd docker 

bash db_setup.sh
```
The bash script creates the database and loads the schema.

### Running the rails server

```
rails s
```

### Common Errors & FAQ

If there is a pending migration error, run this command:

```
rake db:migrate
```

## Getting Started with Docker

### Prerequisites

Since the applciation has been containerized through docker-compose, you would need docker-compose.

### Installing & Running the Containers

To build the container(this is a one time build):

```
sudo docker-compose build
```

To run the container (everytime you want to start the application):

```
sudo docker-compose up
```

You can press ctrl/command + C on the terminal to stop the container.

### Accessing the Rails Container

To access the Rails Container(make sure the containers are already running):

```
sudo bash docker_shell.sh
```
If you want to access the rails console, then run the following command after the previous one:

```
rails c
```

### Accessing the Postgres Container

To access the Postgres Container(make sure the containers are already running):

```
sudo bash db_shell.sh
```

Then type:

```
psql project_matching_development projectmatch projectmatchpass
```

### Automatic Testing with Guard

We're using the [guard-minitest gem](https://github.com/guard/guard-minitest) for automatic testing.
It essentially listens for changes in the specified files and runs minitests.

The `Guardfile` specifies which files `guard` watches and how. To add new files/directories, edit this file.

To use guard, after starting the server with 
```bash
rails s
``` 

run:
```ruby
bundle exec guard
```

This will execute the Guardfile and establish the file watchers.

### Common Errors & FAQ

In case of a database not found or database not created error:

Access the Rails Container and run:

```
cd docker

bash db_setup.sh
```

If you want to reset the container and want to rebuild it, run:

```
sudo docker-compose down
```

and then rebuild it with docker-compose build


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details



