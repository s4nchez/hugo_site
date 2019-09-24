---
layout: post
date: "2008-01-02 09:55:42"
disquss_thread_id: 41421328
title: "Deploying Ruby on Rails as J2EE application"
category: archive
---
If you haven't tried 
[Ruby on Rails](http://www.rubyonrails.org/) because was too busy developing your J2EE applications, now you have no more excuses! It's possible (and surprisingly simple) to deploy a RoR application in your favorite J2EE server just by following these few steps:


## 1. Install JRuby on Rails

[Get JRuby](http://jruby.codehaus.org/Getting+Started) and install the Ruby on Rails
[gem](http://rubygems.org/read/book/1):

```bash
gem install rails --include-dependencies --no-rdoc --no-ri
```

## 2. Create a simple test application

Run the following commands to set up your new application:

```bash
rails test_app
cd test_app
```

You'll have to edit the first line of the created scripts (**'script**' directory) to use JRuby:

```bash
#!/usr/bin/env jruby
```

And at this point you're ready to test your application:

```bash
script/server
```

Open 
[http://localhost:3000](http://localhost:3000) and check if your application is running as it should.

Now let's create some functionality. First, edit your **config/database.yml** file, defining your development and production database as it follows. Note that we don't need the test database and we can use the same database for both development and production  for the scope of this example:

```yaml
adapter: mysql
database: test_app
user: root
password: xxx
host: localhost
```

Create a [scaffold](http://en.wikipedia.org/wiki/Scaffold_%28programming%29):

```bash
script/generate scaffold Dog name:string
rake db:drop:all
rake db:create:all
rake db:migrate
```

At this point you're already able to point your browser to [http://localhost:3000/dogs](http://localhost:3000/dogs) and start playing with with your database.

## 3. Install the JDBC adapter and change your application

In order to deploy as a Java web application, you'll have to replace the database adapter by a JDBC one. To achieve this, first you need a new gem:

```bash
gem install activerecord-jdbc-adapter --no-rdoc --no-ri
```

You also need to copy your mysql driver (JAR file) to your **JRUBY_HOME/lib** directory and edit your **database.yml** once more:

```yaml
adapter: jdbc
driver: com.mysql.jdbc.Driver
url: jdbc:mysql://localhost/test_app
username: root
password: xxx
host: localhost
```

Restart your server and, since we just changed its configuration, everything should be still working exactly as before.

## 4. Install Goldspike and create your WAR file

In your application directory, install the [plugin](http://wiki.jruby.org/wiki/Goldspike):

```bash
script/plugin install http://jruby-extras.rubyforge.org/svn/trunk/rails-integration/plugins/goldspike
```

To include your database driver in the generated archive, you have a few options (Maven is one of them), but for now let's just copy it to the '**WEB-INF/lib**' directory of the application:

```bash
mkdir WEB-INF/lib
cp $JRUBY_HOME/lib/mysql-connector-java-5.0.5-bin.jar WEB-INF/lib
```

You also need to edit the **app/controllers/application.rb** file and include the line:

```bash
protect_from_forgery :secret => '6dc47d156f8f3724e4634c37bc0f9f94'
```

Finally, to create your WAR file, run:

```bash
rake war:standalone:create
```

Deploy the generated file in your favorite J2EE server like Tomcat or WebLogic.

## Conclusion

The integration between Ruby on Rails and Java is easier than most people would expect, and it may become a new option to develop your next web application. That may be also a great motivation to learn JRuby and start taking advantage of its [integration with existing Java code](http://jruby.codehaus.org/Java+Integration).
